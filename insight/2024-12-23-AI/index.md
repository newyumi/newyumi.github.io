---
layout: post
title: "AI에 대한 정보 수집"
subtitle: "이제는 더 자세히 알아야할 것 같아"
type: ""
# insight: true
text: true
author: "Yumi Yang"
post-header: false
header-img: ""
# order: 7
date: 2024-02-10
comments: true
---

[생성 AI 덕분에 진성고객, 충성고객 늘어난다 - 티타임즈 유튜브](https://youtu.be/JiFU2B44edc?si=28N42o-S98uBOy7v)
배민 야놀자 쏘카 서비스에서 G AI가 어떻게 적용되는지 정리해준 영상인데 예시들이 재미있다.

[해당 영상에 대한 정리와 RAG 관련된 내용](https://brunch.co.kr/@ericpm/5)

시대를 꿰뚫는 불타오르듯이 따라가는 화두 - 메타버스, 블록체인 등
제대로 활용해서 혁신을 이룬 곳이 있긴 하지만 굳이 필요하지 않은 부분에서도 사용한 사례가 많았었다.

지금 생성AI는 패러다임 시프트가 실제로 일어나고 있고, 눈으로 볼 수 있는 결과들이 나오고 있다.

할루시네이션에 대한 걱정들이 있었음 - AI에서 할루시네이션은 사람이 경험하는 환각과 비슷하게, 모델이 없는 사실을 만들어내거나 현실과 다른 내용을 생성하는 현상
사실과 다른 정보, 완전히 허구의 내용, 왜곡된 컨텐츠 생성.
원인은 데이터 품질 문제, 확률 기반 생성, 컨텍스트 부족, 목표와 평가 메트릭 등
이 부분 해결방법 - 첫 도입을 내부에서 하고, 내부 직원들 대상으로 테스트 이후 대고객 서비스로 파이를 키우는 방법

잘하고 있는 서비스에 다른 곳에서 줄 수 없는 고객 경험을 주는 방향으로 전략을 짜라
퍼포먼스 성능을 높이거나 비용에 변화를 주는 방향이 있고, 또는 아에 새로운 서비스 개발

인덱싱 벡터검색
오타가 난 것도 검색을 해주고, 컨텍스트에 맞게 검색을 해줄 수 있다
e커머스에서는 검색이 돈이다

모델 정보
GPT-4o
OpenAI-o1 추론을 강화학습으로 더 보완한 모델 - 사람처럼 시간을 할애하여 생각하는 시간을 가진다는 특징이 있음
[Korean Cipher with OpenAI o1](https://www.youtube.com/watch?v=eZDmDn6Iq9Y) - 한국어 암호화 방식도 추론가능
처음으로 gpt 이름이 아닌 o1
[OpenAi o1에 대한 흥미로운 사실 7가지](https://yozm.wishket.com/magazine/detail/2784/)

구글 Gemini 2.0 [오픈AI 'o1' 대항마 떴다…구글, 추론 전용 AI 모델 공개](https://www.aipostkorea.com/news/articleView.html?idxno=5364&fbclid=IwY2xjawHU-_5leHRuA2FlbQIxMQABHR-uzrXc6GDZcApkGBbaEkaVqtgpjEBC3IczneFA51s_rBmgHlhfHUD2oA_aem_pxOo3mXsV6wrHafeSCZceQ)

[OpenVoice V2](https://github.com/myshell-ai/OpenVoice)

랭체인 https://brunch.co.kr/@ywkim36/147
RAG 
텍스트 파일을 올리면 LLM이 이해가능한 벡터로 변환해서 저장해두는 기능을 제공하는 LLM 서비스들이 있어 거기에 2MB 정도 텍스트 파일을 올려두면 내 질문에 답을 할때 AI가 벡터 저장소에서 검색을 하고 해당 내용을 바탕으로 질문에 답을 해 그걸 RAG 기술이라고 부름
우리 같은 경우, 작업 중인 소스파일 레포지토리를 벡터저장소에 올려두고 질문을 할 수 있겠지 - 파일베이스 검색과는 다른데 이미 벡터 형태로 변환된 상태를 쓸거야 아마

SLM이라고 작게 언어모델을 만들어서 파인튜닝하는게 유행이래 Ollama 다운받음

파인튜닝 관련
https://www.sktenterprise.com/bizInsight/blogDetail/dev/11003?utm_source=fb&utm_medium=feed&utm_campaign=branding&utm_content=axolotl_241217&fbclid=IwZXh0bgNhZW0BMABhZGlkAasZ47PNqVMBHWZ0fPZgsah9_YKrYmDPGtyhD17aJQEM6scZKXXOeNVTAaizTXRIJV5cTQ_aem_mMQXWIcHiNTSNN6tsKTpyw&utm_id=120217899822830595&utm_term=120218280808400595
https://devocean.sk.com/search/techBoardDetail.do?ID=166098&boardType=&query=no-code&searchData=&page=&subIndex= 


https://www.facebook.com/share/14uDmceGhk/ 