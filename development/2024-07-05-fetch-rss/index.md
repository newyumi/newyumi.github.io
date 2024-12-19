---
layout: post
title: "Next.js 프레임워크를 이용하여 DynamoDB에 RSS feed 데이터 저장하기"
subtitle: "#nextjs api"
type: "Backend"
development: true
text: true
author: "Yumi Yang"
post-header: false
header-img: ""
order: 13
date: 2024-07-05
comments: true
---

Next.js를 이용해서 개발하다보니, 이 프레임워크는 API도 만들 수 있다해서 사용해보고 싶었다.

항상 RDB만 사용하다보니 NoSQL도 사용해보고 싶어서 AWS에서 제공하는 완전 관리형 데이터베이스인 DynamoDB를 사용해보기로 했다.

데이터 모델이 유연해서 데이터마다 필드가 다 달라도 되는걸 알고 있었지만, 직접 경험해보니 더 재밌고 새롭게 느껴졌다.

리스트를 불러올 때 페이지네이션을 적용하고 싶어서 찾아보니 스캔을 많이 쓰긴하던데 모든 항목을 검색해서 비효율적인것 같아 `LastEvaluatedKey` 라는걸 이용했다.

API 결과에서 마지막 값을 저장하고, API 콜 할 때 저장한 값을 `ExclusiveStartKey`에 담아서 보내면, 해당 데이터의 다음 데이터부터 응답을 주는 방식으로 익숙한 방식인데 형식을 그대로 보내야 하는걸 몰라서 시간이 좀 걸렸다.

`ScanIndexForward는` true 이면 sort key가 오름차순, false 이면 내림차순

sork key는 테이블 생성시 설정해주는데 수정이 안되니 처음에 PK, sork key 설정을 잘 해주는게 좋다.

xml 데이터를 파싱해서 DB에 저장하기만 하면 된다. Next.js 프레임워크를 이용해서 route를 간단히 만들어주니 편리하다. 이제 프론트엔드 개발자도 API 만드는게 어렵지 않게 되었다.

<br/>

```javascript
import Parser from "rss-parser";
import { writeToDynamoDB } from "../../../utils/dynamodb";
import { NextRequest, NextResponse } from "next/server";
import { v4 as uuidv4 } from "uuid";

import "server-only";

const parser = new Parser();

function extractImageUrl(item: any): string | null {
  if (item.enclosure && item.enclosure.url) {
    return item.enclosure.url;
  } else if (item["media:content"] && item["media:content"].$ && item["media:content"].$.url) {
    return item["media:content"].$.url;
  } else {
    const match = item.content.match(/<img[^>]+src="([^">]+)"/);
    return match ? match[1] : null;
  }
}

async function processRSSFeed(feedUrl: string): Promise<any[]> {
  try {
    const feed = await parser.parseURL(feedUrl);

    const newsItems = feed.items.map((item: any) => ({
      Id: uuidv4(),
      Author: item["author"] ? item["author"] : item["dc:creator"] ? item["dc:creator"] : "",
      Link: item.link ? item.link : "",
      PubDate: item.pubDate ? new Date(item.pubDate).toISOString() : "",
      Source: feed.title ? feed.title : "",
      Title: item.title ? item.title : "",
      Tags: item.categories ? item.categories.join(",") : "",
      CreatedDate: new Date().toISOString(),
      Categories: item.categories ? item.categories : "",
      Content: item.content ? item.content : "",
      Image: extractImageUrl(item),
    }));

    console.log("Processed news items:", newsItems);
    writeToDynamoDB("News", newsItems);

    return newsItems;
  } catch (error: any) {
    throw new Error(`Error processing RSS Feed (${feedUrl}): ${error.message}`);
  }
}

export async function GET(req: NextRequest) {
  const feedUrls = ["https://techcrunch.com/feed", "https://www.theverge.com/rss/index.xml"];

  try {
    const processedItems: any[] = [];
    for (const feedUrl of feedUrls) {
      const items = await processRSSFeed(feedUrl);
      processedItems.push(...items);
    }

    return NextResponse.json({ message: "RSS Feeds successfully processed", data: processedItems });
  } catch (error: any) {
    return NextResponse.json({ message: `Error processing RSS Feeds: ${error.message}` });
  }
}

```

간단하게 구현해보면서 들었던 생각인데, 예전에 php 언어로 웹 개발을 할 때 한 명의 개발자가 프론트와 백엔드를 모두 처리했던 것처럼 이제는 프론트엔드 툴이 많이 발전하면서 비슷한 흐름이 다시 나타나는 것 같다. 결국 풀스택 개발자라는 개념이 더 두드러지고 수요가 많아지지 않을까 싶기도하다.
