---
layout: post
title: "2020년도 Front-end 개발 방향에 대해"
subtitle: "#font-end"
# type: "Have to study"
development: true
text: true
author: "Yumi Yang"
post-header: false
header-img: ""
order: 7
date: 2020-05-05
comments: true
---

계속 되었던 고민 중에 하나가 - 프론트엔드 개발자로 깊이 있게 공부해 나아갈 것인가, 또는 소위 풀스택 개발자라고 하는, 웹에 관련하여 처음부터 끝까지 혼자 웹프로그램을 하나 만들 수 있는 개발자가 되어야 할 것이였다. 멀티태스커이면서 어떤 분야에서는 스페셜리스트가 된다면야 바랄게 없지만, 나의 방향은 하나라도 잘한다 말할 수 있을 스페셜리스트가 되고 싶더라. 해외에서 지내고 있는 관계로 링크드인에서 영어권 국가의 프론트엔드 개발자 구인 관련된 글이 소개되고는 하는데, 최근 동향은 어떤지 살펴보고자 회사들 채용정보를 가끔씩 살펴 보고 있다.

[works hub](https://www.works-hub.com/)라는 사이트를 알게 되었다. 사이트 내에 직종별로 분류가 되어있는데, 그 중 [javascript works](https://javascript.works-hub.com/) 페이지를 즐겨찾기 해 두었다. 디자인이 멋있기도하고 고급 개발자를 모집하는 회사들이 많아 가끔씩 들여다보고 있다. 몇 몇 회사의 채용공고들을 보면서, 요새 회사가 필요로 하는 능력과 경험들은 이렇구나 - 생각하면서 나한테 필요한 것들을 모아두고, 공부의 방향을 잡아봤다.

<br/><br/>

## What kind of experience are we looking for?

### Experience & Skills

- You have solid JavaScript, HTML, LESS/CSS experience and have experience with at least one front end framework (e.g. React, Vue, Angular, etc) and building SPAs (including setting up tooling like Webpack and Babel

- solid experience with React/Redux and Typescript or ES6

ES6로 개발을 하고 있는데, Typescript는 필요하면 그때 그때 찾아서 쓰고 있는데 기본적인 것들은 익혀둬야 되겠다. 그리고 LESS/CSS를 기본적인 CSS를 기준으로 정확한 개념없이 혼용해서 사용한 적이 많은데, LESS, SCSS, SASS의 정확한 차이와 문법을 정리를 해둬야겠다.
그리고 최근에 회사에서 모든 프로젝트를 React로 개발하고 있는데, 리액트 하면 리덕트지. 리덕트 계속 팔 것.
웹팩이나 바벨 또한 기존의 것들을 커스텀하거나 정확한 내용은 무시하고 쓴 적도 많았는데, 관련 파일을 스스로 만들어봐야겠다.

<br/>
### Problem solver

You enjoy working collaboratively in a team, but can also work independently to solve complex problems. You seek help/feedback when required to ensure solutions are robust, performant, secure, etc… utilising product managers, test engineers and SRE’s.

여기서 SRE’s 라는걸 처음 봐서 검색해보니 사이트 신뢰성 공학 (Site Reliability Engineering)이라는게 등장했다.
사이트 신뢰성 공학은 소프트웨어 공학의 관점들을 통합한 원칙으로, 이들을 인프라스트럭처와 운영 문제에 적용한다. 주된 목적은 상당한 스케일링이 가능하고 상당히 신뢰할만한 소프트웨어 시스템을 만드는 것이다.

Site Reliability Engineering (SRE) is a discipline that incorporates aspects of software engineering and applies them to infrastructure and operations problems. The main goals are to create scalable and highly reliable software systems.

관련 질문으로 What is the difference between SRE and DevOps? 가 있었는데,
A major difference between SRE and DevOps is the focus on coding and type of environment you are in. ... DevOps share common ground with SRE as a DevOps engineer is the top of the pyramid, architecting both a culture and a system to automate the delivery of infrastructure or tasks within the development process. 라고 하네.

더 찾아보니, 또 조대협의 블로그가 나왔다. ㅋㅋㅋ 검색하다보면, 자주 나오는 분들이 있다. 감사한 분들.
https://bcho.tistory.com/1325 역시나 정리가 잘 되어 있다.

<br/><br/>
한국에서는 유니콘 회사들의 채용 공고를 찾아보곤 한다. 노션으로 회사를 소개하는 것도 취저 👍🏻
그 중 최근 투자로 유명한 회사의 프론트엔드 개발자를 살펴보면 다음과 같다.

1. **주요 업무**
   - 모바일 웹뷰 기반의 다양한 사업팀 Product 개발
     - 신규 사업, 광고, 지급 결제 등
   - 동네 모임 서비스 개발
   - UI/UX 개선
2. **자격 요건**
   - HTML, CSS 및 JavaScript(Node.js) 생태계에 익숙하신 분
   - TypeScript, Flow 등 JS 정적 타이핑 툴 경험
   - SPA(React, Vue, Angular 등) 프로젝트 개발 경험
   - UI/UX에 관심이 많고 고민을 좋아 하시는 분
   - Git 및 GitHub 기반 협업에 능숙하신 분
   - 서버 개발자, 디자인 직군과 원활히 소통하는 능력
   - 새로운 기술에 관심이 많고, 자기 개발을 위해 노력하시는 분
3. **우대 사항**
   - Flux 등 상태 관리 패턴에 대한 이해가 깊으신 분
   - Webpack, Rollup 등 모듈 번들러에 대한 이해가 깊으신 분
   - SPA Framework을 이용한 SSR 프로젝트 경험
   - 모바일 또는 반응형 웹 개발 경험
   - Node.js 등 서버 개발 경험
   - 오픈소스 Contribution 경험
   - GraphQL에 대한 이해
4. **기술 스택**
   - React, Next.js, MobX, Apollo Client
   - Vue, Vuex
   - TypeScript
   - Styled Component, SASS

<br/>
보면서 자격요건에는 부합하니, 우대 사항에도 부합하고 싶어지는데.
역시나 상태관리 패턴이 첫번째다. 나의 경우, React 프로젝트에 처음부터 개발에 투입된게 아니라 수정하는 단계부터 합류하게 되면서,
짜여진 구조에서 상태관리를 접해볼 기회가 있었다. 정답은 모르겠지만, 주어진 코드를 보면서 익히게 되어 리액트에서 상태관리가 왜 필요한지,
어떻게 사용해야 되는지를 배웠다. 이제 거꾸로 개념을 한 번 짚고 넘어갈 때가 된 것 같다.
이 회사에서는 GraphQL을 쓰고 있는지 궁금. 처음 React를 찾아볼 때, 공식 홈페이지에서 Toolchains을 추천해주는 문구를 보고, 또 Gatsby로 이것저것 해봤는데,
개츠비는 적극적으로 GraphQL을 사용한다. 프론트엔드 개발자로써 종종 API 개발에 눈 독 들이게 되는데, GraphQL을 사용하면 내가 쿼리를 날릴 수 있겠다 싶어
매력적인 툴이구나 생각했었다. 이 것도 써봐야겠다.

<br/><br/>
보다 보면, 역시 대세는 리액트 인가. 할 정도로 리액트를 사용하는 회사가 많았다. 앵귤러1 이후에 뷰와 리액트에서 고민하다가 리액트로 프로젝트들을 개발하기 시작했는데, 잘 한 선택이구나 싶다. 당분간은 계속해서 리액트의 시대가 아닐까. 뭐 대체적으로 많이 다르지 않기도 하지만, 발을 담가보는건 또 다른일이니.
언제나 공부해야될 것들은 많지만, 방향을 계속해서 잘 잡아나가는 것도 중요한 것 같다.

<br/><br/>
