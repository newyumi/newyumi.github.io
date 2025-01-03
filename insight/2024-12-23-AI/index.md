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
date: 2024-12-30
comments: true
---

기술들은 매일같이 발전하고 있지만 이전에 블록체인이나 메타버스와 같이 조금은 어렵고 실생활에서 사용하지 않을 수 있었던 기술과는 달리, AI는 너무나 많이 회자되고 적용하는 회사들이 넘쳐나고 너도나도 사용중으로 느껴진다.
나도 접하고부터는 매일 ChatGPT를 사용하고 Cursor AI 에디터를 사용해서 개발하고 있는 지금, 이제는 AI에 대해 몰라서는 안되고 자세히 알아봐야할 시기라고 생각된다.
새로운 테크놀로지를 이해하기 위해서는 바로 그 이전의 기술에 대한 이해가 필요하고, 그 흐름을 한 번 놓치면. 생각의 속도는 영원히 뒤쳐진다. 라는 빌게이츠의 말이 피부로 와닿는 시간이다.
알고 싶은 내용들을 찾아보았고 유튜브 브런치 등의 글에서 보고 필요한 내용을 정리한 글이다.


### 서비스에 사용되고 있는 AI
[생성 AI 덕분에 진성고객, 충성고객 늘어난다 - 티타임즈 유튜브](https://youtu.be/JiFU2B44edc?si=28N42o-S98uBOy7v)
[해당 영상에 대한 정리와 RAG 관련된 내용](https://brunch.co.kr/@ericpm/5)

배민 야놀자 쏘카 서비스에서 생성형 AI가 어떻게 적용되는지 정리해준 영상인데 예시들이 재미있다.
방대한 데이터를 바탕으로 개인에게 맞춤으로 메뉴나 숙소를 추천해주거나 데이터가 적다면 간단한 키워드를 통해 리뷰를 작성하게끔 유도하는 서비스들이 생겨나고 있다. 쏘카의 경우는 24시간 고객 센터를 운영하고 있는데, 지금까지의 방대한 응대 매뉴얼을 생성형 AI에 도입해서 기존의 챗봇과는 비교할 수 없는 개인 맞춤형 응대가 가능한 AI 응대가 가능한 서비스를 개발했다고 한다. 지금은 투자 비용이 높지만 결과적으로 어떻게 수익으로 연결될지 궁금한 부분이다.


### 생성형 AI 도입 방안
AI에서 할루시네이션에 대한 걱정들이 있었다. AI에서 할루시네이션은 사람이 경험하는 환각과 비슷하게, 모델이 없는 사실을 만들어내거나 현실과 다른 내용을 생성하는 현상으로 사실과 다른 정보, 완전히 허구의 내용, 왜곡된 컨텐츠 생성의 케이스로 나뉘어진다.
원인은 데이터 품질 문제, 확률 기반 생성, 컨텍스트 부족, 목표와 평가 메트릭 등으로 인한 것이다.
이러한 문제를 극복하고 서비스에 AI를 도입하는 해결방법으로 첫 도입을 내부에서 하고, 내부 직원들 대상으로 테스트 이후 대고객 서비스로 파이를 키우는 방법이 있다.

도입 전략으로는 잘하고 있는 서비스에 다른 곳에서 줄 수 없는 고객 경험을 주는 방향으로 전략을 짜거나,
퍼포먼스 성능을 높이거나 비용에 변화를 주는 방향이 있다. 또는 아에 새로운 서비스를 개발하는 것.

e커머스에서는 검색이 돈이다. 검색이 중요한데 AI에서 벡터 검색과 인덱싱을 통해 검색의 정확성과 유연성을 크게 향상시킬 수 있다.
벡터 검색은 텍스트나 이미지를 벡터로 변환하는데, 임베딩된 벡터는 데이터의 의미적 정보를 내포하고 데이터 간의 관계를 수학적으로 표현 가능하다.
검색 시 가까운 벡터를 찾을 수 있어서 문맥 기반 검색이 가능하다. 따라서 오타가 난 것도 검색을 해주고, 컨텍스트에 맞게 검색을 해줄 수 있다.
인덱싱은 대규모 벡터를 효율적으로 검색할 수 있도록 데이터베이스에서 벡터를 저장하는 방법이고, 이를 통해 벡터 간의 유사성 검색을 빠르게 수행할 수 있다.

데이터베이스 인덱싱이 떠올라서 차이점을 찾아봤다.

### 인덱싱 차이점

| **특징**            | **데이터베이스 인덱싱**                             | **AI 인덱싱 (벡터 검색)**                        |
|----------------------|----------------------------------------------------|-------------------------------------------------|
| **목표**             | 빠른 데이터 검색 및 CRUD 연산 최적화               | 의미적 유사성 기반의 검색 (텍스트, 이미지 등)   |
| **데이터 형태**      | 관계형 데이터, 숫자, 문자열 등의 정형 데이터      | 텍스트, 이미지, 음성 등 고차원 벡터 데이터      |
| **인덱싱 방식**      | B-tree, Hash, R-tree 등                           | 벡터화된 데이터 (임베딩) 및 벡터 데이터베이스     |
| **검색 방식**        | 정확한 값 검색 (예: "ID = 123")                    | 유사도 기반 검색 (예: "이 문장과 비슷한 문서")    |
| **용도**             | 데이터베이스 쿼리 성능 최적화                      | AI 모델에 의한 의미적 유사성 검색                |



### 내가 알고 있는 최신 AI 모델 정보
모델 정보
GPT-4o (o: omni)
OpenAI-o1 추론을 강화학습으로 더 보완한 모델로 사람처럼 시간을 할애하여 생각하는 시간을 가진다는 특징이 있다.

OpenAI가 'o1' 모델에 'GPT'라는 명칭을 사용하지 않은 이유는, 이 모델이 기존의 GPT 시리즈와는 다른 새로운 패러다임을 대표하기 때문.
'o1' 명칭의 의미와 배경
- 새로운 시작을 의미: OpenAI는 이 모델이 추론에 특화된 첫 번째 모델이기 때문에, 기존의 'GPT'라는 이름을 버리고 새롭게 시작하는 의미에서 'o1'이라 명명함.
- 상호보완적 모델: 'o1'은 GPT-4o를 대체하는 모델이 아니며, 상호보완적인 모델로 목적에 맞게 사용하는 것이 더 효과적이다.
- 추론 중심 모델: 'o1'은 복잡한 추론에 특화된 모델로, 기존의 GPT 시리즈와는 다른 목적과 기능을 가지고 있음.


### 관련된 흥미로운 내용들

[Korean Cipher with OpenAI o1](https://www.youtube.com/watch?v=eZDmDn6Iq9Y) - 한국어 암호화 방식도 추론가능하다는 영상인데, 한국인들이 외국인들이 번역할 수 없게끔 한국인만 알아볼 수 있는 한글을 써서 리뷰한 내용도 이제는 추론이 가능하다는 것. 해당 영상 데모를 진행했던 연구원이 쓴 댓글인데, 한글 암호 해독 방식을 직접 가르치지 않고 추론만을 가르쳤음에도 불구하고 그 능력이 저절로 가능해졌다는 점을 전달하고 싶었다고 하셨다.

처음으로 gpt 이름이 아닌 o1 - [OpenAi o1에 대한 흥미로운 사실 7가지](https://yozm.wishket.com/magazine/detail/2784/)

구글 Gemini 2.0 [오픈AI 'o1' 대항마 떴다…구글, 추론 전용 AI 모델 공개](https://www.aipostkorea.com/news/articleView.html?idxno=5364&fbclid=IwY2xjawHU-_5leHRuA2FlbQIxMQABHR-uzrXc6GDZcApkGBbaEkaVqtgpjEBC3IczneFA51s_rBmgHlhfHUD2oA_aem_pxOo3mXsV6wrHafeSCZceQ)

제미나이 쓰는 분들도 많던데, 경쟁적으로 개발되고 쓸 수 있는 생성형 AI가 많으니 소비자로써는 좋다.
추론형이 확실히 답변이 좋아서 돌아가면서 사용중인데 개인적으로는 o1이 가장 만족도가 높음.


### RAG (Retrieval-Augmented Generation)

[검색 증강 생성(RAG)이란 무엇인가요?](https://aws.amazon.com/ko/what-is/retrieval-augmented-generation/)

지금 LLM이 어디에나 있고 매일같이 학습자료를 삼키고 있지만, 특정한 날짜를 기준으로 학습한 것을 끊어서 서비스를 내놓게 되는데 그러면 가장 최신의 정보를 학습하지 못하게 된다. LLM을 보다 정확하고 최신의 상태로 유지하려는 프레임워크를 

LLM은 Large Language Model의 약자로, 방대한 데이터와 최신 딥러닝 기술을 활용하여 자연어를 이해하고 생성할 수 있는 언어 모델

RAG 
텍스트 파일을 올리면 LLM이 이해가능한 벡터로 변환해서 저장해두는 기능을 제공하는 LLM 서비스들이 있어 거기에 2MB 정도 텍스트 파일을 올려두면 내 질문에 답을 할때 AI가 벡터 저장소에서 검색을 하고 해당 내용을 바탕으로 질문에 답을 해 그걸 RAG 기술이라고 부름
우리 같은 경우, 작업 중인 소스파일 레포지토리를 벡터저장소에 올려두고 질문을 할 수 있겠지 - 파일베이스 검색과는 다른데 이미 벡터 형태로 변환된 상태를 쓸거야 아마

SLM이라고 작게 언어모델을 만들어서 파인튜닝하는게 유행이래 Ollama 다운받음

[No-Code LLM 파인튜닝 : Axolotl](https://www.sktenterprise.com/bizInsight/blogDetail/dev/11003?utm_source=fb&utm_medium=feed&utm_campaign=branding&utm_content=axolotl_241217&fbclid=IwZXh0bgNhZW0BMABhZGlkAasZ47PNqVMBHWZ0fPZgsah9_YKrYmDPGtyhD17aJQEM6scZKXXOeNVTAaizTXRIJV5cTQ_aem_mMQXWIcHiNTSNN6tsKTpyw&utm_id=120217899822830595&utm_term=120218280808400595)
[No-Code LLM 파인튜닝 : LLaMA-Factory](https://devocean.sk.com/search/techBoardDetail.do?ID=166098&boardType=&query=no-code&searchData=&page=&subIndex= )


https://www.facebook.com/share/14uDmceGhk/ 


프로젝트 매니지먼트 책이 도움이 됐었는데, 저자가 AI에 쓴 글도 정리가 무척 잘되어있다.
모놀리틱 모델과 컴파운드 시스템
가장 인기있고 일반적으로 사용되는 컴파운드 AI 시스템 중 하나가 바로 검색 증강 생성(RAG)이다.
[AI 에이전트](https://brunch.co.kr/@ywkim36/160)
[LAG 이해하기](https://brunch.co.kr/@ywkim36/146)
[Langchain 이해하기](https://brunch.co.kr/@ywkim36/147)




### 기타 정보

[OpenVoice V2](https://github.com/myshell-ai/OpenVoice)
OpenVoice는 단지 짧은 오디오 샘플을 이용하여 다양한 언어와 스타일로 음성을 복제할 수 있는 기술을 제공. 이 기술은 TTS(Text-to-Speech) 분야에서 유연한 음성 스타일 제어와 언어간 제로-샷(AI 모델이 사전 학습하지 않은 작업이나 데이터에 대해 바로 수행할 수 있는 능력) 음성 복제를 가능하게 하여, 다양한 상업적 및 창의적 응용에 영향을 미칠 것으로 보입니다.