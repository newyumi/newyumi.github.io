---
draft: true
layout: post
author: "Yumi Yang"
title: "Thing's platform"
subtitle: ""
type: "IoT data management"
projects: true
text: true
portfolio: true
post-header: false
header-img: ""
main-img: ""
target-title: "IoT 상태관리 시스템"
role: "시스템 구조 설계 및 Frontend 개발"
target-specific: "IoT status data system, Web programming"
team: "PM 1, 기술 PM 1, 서비스 기획 1, <br/> Blockchain 2(자문위원 1), Front-end 2, Back-end 1, 디자이너 1"
platforms: "Web"
date: "June 2022 - 2023 현재 진행중"
order: 8
---

☀️ Summary <br/>
콜드체인 과제의 연장으로 콜드체인을 실행하는 다양한 업체와 각 업체가 사용하는 다양한 센서의 데이터를 관리하고, 블록체인 기술을 이용하여 데이터의 위변조를 불가하게 하는 시스템 개발

🌱 Requirements <br/>

- 센서의 위치를 표시하고 각 센서의 스펙 정보 조회
- 각 센서의 Raw 데이터를 보고 싶음
- 센서가 이상이 있는 경우 경고(Alert) 기능
- 원하는 정보를 조회하고 싶음, 예를 들어, A 센서의 이번달 B 데이터의 합

✨ Solution <br/>

- 지도를 이용하여 회사의 위치를 표시하고, 각 회사가 소유하고 있는 센서의 리스트와 각 센서의 스펙을 표시
- 시간순으로 센서의 데이터를 로그 형식으로 표시, 데이터가 매우 많기 때문에 무한 스크롤을 이용했다.
- 센서에서 일정시간 이상 데이터가 오지 않는 경우, 또는 평소 데이터보다 수치가 매우 다른 경우(수치의 이상 범위를 미리 설정해둠)를 심각/경계/주의/관심 등으로 세분화하여 경고 표시했다.
- 메뉴선택 형의 챗봇 형태를 이용하여 미리 유저가 필요할 만한 문구과 대답의 로직을 설정해뒀다.

💐 Performance <br/>

- Technical leader
- RDB 데이터베이스 설계
- 프론트엔드 개발
  <br/> <br/>

![1](img/1.png)
![3](img/3.png)
![4](img/4.png)

대표적인 페이지들이다. 대외비라 내용은 블러처리를 했다.<br><br>

<strong>Things Data Management Platform</strong><br>
TP는 다양한 센서(국제규격을 준수하는 LoRaWAN)를 지원하고, 각 센서의 데이터 및 기기의 상태 관리를 하는 것을 목적으로 한다.
<br>
또한, HyperLedger에 변조불가능하게 저장하는 기능을 제공한다. 실제 데이터의 발생 여부를 확인할 수 있다.
Thing 메시지 형태의 로그를 통해 상시 모니터링 할 수 있는 기능을 제공한다.
<br>
각 Thing의 Metric 정보로 센서의 최신 측정값을 확인할 수 있고, 제어까지 하는 것을 목표로한다.

<ol>
<li> 크게 네트워크 / 어플리케이션 / Thing 으로 구성 - 콜드체인 예시</li>
<li> 센서의 Metric 정보(측정 항목)은 각기 다름. 다른 Metric 정보를 보여주고 제어할 수 있는 부분이 특징임</li>
<li> 이벤트 콘솔 페이지를 이용해서 각 센서에 설정된 이벤트를 한 눈에 파악하고 조치를 취할 수 있음</li>
<li> 봇에 다양한 기능을 추가하여 시스템의 기능을 다양화 할 수 있을 것으로 예상됨 </li>
</ol>
<br>
