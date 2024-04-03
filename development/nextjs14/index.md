---
layout: post
title: "Next.js version 14 Routes"
subtitle: "#next.js #14version #routes"
type: "Framework starter"
development: true
text: true
author: "Yumi Yang"
post-header: false
header-img: ""
order: 11
date: 2024-03-30
comments: true
---

[Routes 예시](https://next-app-directory-chi.vercel.app/) <br/>
[공식문서 - 설명이 엄청 잘되어있다](https://nextjs.org/docs/app/building-your-application/routing/defining-routes)

<br/>

간단한 사용자 관리 사이트를 Next.js로 만들었었는데, 복잡한 화면이 아닌 테이블로 데이터를 보여주는 화면이 많다보니
API를 호출하면서 바로 화면에 보여주니 속도가 빠르다는게 확 체감되었다.
이후로 사용자나 센서 관리와 같은 정형화된 데이터들을 관리하는 페이지를 만들때는 Next.js를 사용하고 있다.

`Server side rendering`(Also referred to as "SSR" or "Dynamic Rendering")은 서버가 HTML 파일을 만들어 보내주면 브라우저가 받고, 이후 JS 파일을 다운받아서 React를 실행한다. 이 후 페이지가 작동되어 첫페이지 로딩속도가 빠르고 검색엔진 최적화가 가능하단 점이 장점이다. 그러나 초기 로딩 이후 페이지 이동 시 CSR에 비해 느리고, 깜빡임 이슈가 있을 수 있다.

SEO가 중요한 웹사이트나 초기 로딩 시간이 매우 중요한 웹에서는 SSR이 더 적합하다. 이 경우 서버 부하가 높아지고 개발 서버와 클라이언트 로직이 분리되어 있어 개발 복잡도는 증가할 수 있다. 서버 부하가 많을 수 있거나 동적인 UI, UX가 중요한 경우는 CSR이 낫다.

<br/>

현재(2024년 04월) Latest 버전인 14에서 라우트가 변경된 부분들이 있어 소개한다.
구조적으로 변경된 점은 라우팅하는 폴더마다 layout, page 2개의 파일이 꼭 있어야 한다는 점이다.
이를 기반으로 여러가지 방법으로 레이아웃을 구성할 수 있는데, Grouped layout / Nested layouts / Parellel routes를 만드는 방법을 살펴보자.

### Route group

폴더이름을 괄호를 이용해서 (그룹이름)으로 작성 가능하나 외부에서는 알 수 없다. 따라서 URL에 영향을 주지 않는다. 대체로 그룹 폴더 아래에 폴더들을 만들어 주소화한다. 하이라키가 같으나 다른 레이아웃을 만들 때 유용하게 쓸 수 있다.

### Nested layouts

Dynamic routes 방법을 사용하면 되는데, [slug]로 폴더 이름을 작성 할 수 있다. [slug] 슬러그는 동적경로이며 parameter에 따라 변경된다. 주소는 /[slug]로 파라미터로 `blog`를 넘기면 /blog가 되는것. yarn build 하면 정적으로 파일이 생성된다. 슬러그는 웹 사이트의 특정 페이지를 쉽게 읽을 수 있는 형태로 식별하는 URL의 일부

### Parellel routes

폴더명에 @slot을 붙인다.

- app/layout.js, app/page.js
- app/@team/pages.js
- app/@analytics/pages.js
  team, analytics 페이지를 app/layout에서 병렬로 보여지도록 설정할 수 있다.

@슬롯: 슬롯은 라우트 세그먼트가 아니며, URL 구조에 영향을 주지 않는다. 내부적으로 그룹화명 (그룹이름)은 내부에서만 사용하고 외부에서는 드러나지 않는다. 파일 경로 /@team/members는 /members에서 접근할 수 있지만!

<span style="color: orange">
Soft Navigation으로만 이동 가능하다. Hard Navigation(주소로 접근)으로 이동시 404 에러 페이지가 뜬다. 전체 페이지 재렌더링이 필요한 Hard Navigation에서 Next.js는 먼저 일치하지 않는 슬롯의 default.js 파일을 렌더링하려고 시도하고, 사용할 수 없는 경우 404를 렌더링한다.
</span>

<br/>
SSR이지만 다양한 레이아웃을 구성할 수 있으므로 적절하게 사용하면 UI가 복잡해지더라도 빠른 속도의 웹페이지를 개발할 수 있을 것으로 기대된다.
