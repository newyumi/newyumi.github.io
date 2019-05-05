---
layout: post
author: "Yumi Yang"
title:  "TOC project"
subtitle: "Top Operation Control System"
type: "Energy Monitoring"
projects: true
text: true
portfolio: true
post-header: false
header-img: "img/toc-main.png"
main-img: "toc/img/toc1.png"
target-title: "에너지 시스템 모니터링을 위한 웹 프로그램 개발"
target-specific: "Energy monitoring system, Web programming"
team: "엔지니어 5명, 디자이너 1명"
platforms: "Web"
date: "June 2018 - Dec 2018"
order: 1
---

# Background

## CONCORDIA

![toc1](img/toc1.png)

![toc2](img/toc2.png)
###### Structure of TOC

컴퍼니위의 자체 개발 플랫폼인 CONCORDIA는 오픈소스 및 GPU기반의 최적화된 고속 빅데이터 시스템과 기계학습 시스템으로 이루어져 있다.
TOC는 그 프로젝트 중 대표적인 프로그램이다.


# Overview

## Energy Monitoring

TOC는 Total Operation Control의 약자로, 흩어져 있는 사이트들의 전력량과 그에 관련된 정보들을 한 곳에서 모니터링하고 컨트롤 할 수 있도록
만든 시스템이다. 웹 기반으로 되어 있어 통신이 되는 곳에서 접근이 가능하지만 OTP로 등록되어 있는 특정한 유저들만을 위한 시스템이다.

ESS(Energy Storage System) / Solar(태양광) / [DR(Demand Response)](https://en.wikipedia.org/wiki/Demand_response)로 크게 세 종류로 분류되어 있다.
메인 화면에서는 전반적인 각각의 상태를 보여주고, 세부 화면으로 이동할 수 있게 라우팅을 설정하였다.


# Structure

## Language

Node.js 기반으로 Angular1.7.8 버전으로 개발하였다. 처음 일을 시작할 때 앵귤러와 함께 시작해서 앵귤러에 대해 애정이 있지만, 
다음 버전의 Angular는 이전 버전과는 무척이나 다르기 때문에 쉽게 다음 버전으로 넘어가지 못하고 있다. 
아마도 이 프로젝트가 앵귤러를 사용했던 마지막 프로그램이 되지 않을까 싶다.

## 가장 많이 사용하는 라이브러리

프로그램 특성상 차트를 많이 사용하는데, 이번엔 echart를 사용하였다. 종류가 다양하고 커스텀이 용이한편.
그리고 하나의 데이터를 여러모양으로 변환하여 사용하는 경우들이 많아 lodash를 이용하였다.

## Call datas

처음 로딩시에는 RESTful API를 호출하여 DB에 있는 값을 불러오고, 테이블이나 차트와 같은 정형화된 데이터를 사용하는 부분은 5분 단위로 재호출을 하였다.
실시간 데이터가 필요한 부분은 Queue를 사용하여 큐를 받을 때마다 바인딩하여 실시간 값을 유지하였다. (stomp client를 사용)
그리고 페이지를 이동하는 경우에는 interval 객체를 삭제하고, 해당 큐 구독을 취소하였다.

## Map

![map](img/map.png)
###### 위치 이동, 해당 위치에 마커 또는 정보 표시.

우리 회사가 사랑하는 [mapbox](https://www.mapbox.com/). Mapbox GL JS에 유저가 원할만한 기능은 거진 다 있다고 보면 된다. 
기본적인 사용은 무료인데, 상용 프로그램에서 사용하거나 사용량이 많으면 유료로 전환할 수 있다.


<br/><br/>
> Copyright 2018. Companywe. All rights reserved. <br/>
> 이곳의 모든 저작권은 컴퍼니위에게 있습니다. 이곳의 모든 사진들은 허가없이 사용할 수 없습니다.