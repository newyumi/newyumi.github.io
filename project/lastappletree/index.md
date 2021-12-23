---
layout: post
author: "Yumi Yang"
title: "Last apple tree hybrid mobile application"
subtitle: "ionic으로 개발한 협업 모바일 어플리케이션"
type: "Cooperation tool"
projects: true
text: true
portfolio: true
post-header: false
header-img: "img/main.png"
main-img: "lastappletree/img/chat-05.png"
target-title: "업무 협업을 위한 하이브리드 모바일 어플리케이션 개발"
team: "엔지니어 3명, 디자이너 2명"
platforms: "ios, android"
date: "June 2021 - Dec 2021"
order: 5
---

<br/>

기획부터 참여했던 프로젝트고, 기존과 다른 성격의 프로젝트라 재밌게 진행했던 작업이었다.

1. 모바일 인증 - twilio를 사용하여 국제발신 문자 서비스 이용
2. 다국어 - react-intl 이용했고, en/ko 각 파일을 따로 만들어서 코드를 지정하여 다국어 작업 진행.
   device 언어 설정 값을 가지고 와서 default 값으로 지정해주고, 설정에서 언어를 설정할 수 있도록 했다.
3. 소캣 - socket.io-client 이용. 로그인을 하고나면, connect 연결 유무를 확인하여 연결되어 있지 않으면 다시 연결 시도.
4. 시스템 notification에 따른 후처리, 예를 들어 워크보드에 참여중일 때 참여자가 나갔다거나, 파일이 새로 등록됐다 하는 노티를 받으면 그에 따른 화면 처리를 하는 부분.
5. 타임존 - @ionic-native/globalization 으로 사용자 기기의 타임존을 가지고 오고 설정해줌. moment 사용했고, 화면에 표시할때 moment(value).locale(set value).format() 사용, momnet/locale/ 내부에서 필요한 지역 파일을 사용했다.
6. 가장 고생했던 부분은 사진을 다운받을 때 기기 앨범에 저장하는 부분이었는데, blob을 바로 저장할 수 없어서 파일 변환 후 저장했는데, 간단할 것 같았으나 파일에 대한 이해가 없었기도 했고, ionic이 react-native 보단 사용자가 적어서 예시가 많이 없어서 애를 먹었다. <br/>
   다운 받을 때 파일을 write 할 수 있는 권한을 먼저 체크하고, 파일 path를 base64 형식으로 변환한 다음에 capacitor의 Filesystem을 이용해서 파일을 기기에 쓰고, photo library 권한을 write: true로 지정해 준 다음에 저장해줬다. 만들고 나니 별거 아니었는데 고생했던 것만 기억남.

[Last apple tree 홈페이지](https://www.lastappletree.com/) 에서 다운받으실 수 있습니다 👍
<br/><br/>

<div class="lat-images" style="display:flex;width:100%;margin-left:-30px;">
<img src="img/0.2 onboarding.png" width="200"/>
<img src="img/1.1 signup.png" width="200"/>
<img src="img/2 main.png" width="200"/>
<img src="img/2.4 my calendar(left swipe).png" width="200"/>
</div>

<br/><br/>

<div class="lat-images" style="display:flex;width:100%;margin-left:-30px;">
<img src="img/2.5 Inbox(all).png" width="200"/>
<img src="img/3.9 completed workboard.png" width="200"/>
<img src="img/4.2 expand menu(host).png" width="200"/>
<img src="img/4.3 participants.png" width="200"/>
</div>

<br/><br/>

<div class="lat-images" style="display:flex;width:100%;margin-left:-30px;">
<img src="img/4.5.3 reply.png" width="200"/>
<img src="img/4.5.5 final output(list).png" width="200"/>
<img src="img/4.5.6 completed.png" width="200"/>
<img src="img/5 coworkers.png" width="200"/>
</div>

<style>
	.lat-images > img {
		margin-right: 4px !important;
	}
</style>
