# 이어봐 

서비스 주소: https://www.iovar.co.kr/

"이어봐에는 수많은 엔딩이 존재합니다🕵️‍♂️" - 이 순간에도 많은 이야기들이 재생산되고 있습니다. 탐험하세요!

"선택의 길과 마주하세요🧭" - 각각의 선택은 모두 다른 스토리로 이어질 것입니다.

"이야기가 맘에들지 않다구요? 그럼 자신의 스토리로 이어보세요!" - 이어봐에서 상상을 펼쳐보세요.

<br>

## 목차

[기획 동기](#기획-동기)

[사용 스택](#사용-스택)

[시스템 구조](#시스템-구조)

[주요 기능 소개](#주요-기능-소개)

[유저 피드백과 개선 사항](#유저-피드백과-개선-사항)

[개인 별 대표적인 기능 구현](#개인-별-대표적인-기능-구현)

[추가로 구현하는 중인 & 기획중인 기능](#추가로-구현하는-중인-&-기획중인-기능)

<br>

## 기획 동기
모두가 함께 만드는 미연시 재밌지 않을까? 그런 생각으로 기획을 시작했습니다.
초기 기획 단계에 사용자의 참여를 핵심 가치로 생각하고, 기획의 방향을 릴레이 소설의 게임화로 하게되었습니다.

<br>

## 사용 스택
프로젝트 기간이 5주였기에 생산성에 초점을 맞추고 기술 스택을 선정하였습니다. 각 기술 스택 선정의 이유는 다음과 같습니다.

### [FE] **React**  
 1. 스토리를 즐기는 플랫폼이기에 사용자 경험을 위해 SPA 라이브러리/프레임워크 고려
 2. 팀 구성원 모두 SPA 기반 지식이 없었기에 가장 커뮤니티가 큰 React 선정

### [BE] **Node.js**
 1. Node.js를 사용하면 JavaScript만을 사용해서 FE뿐만 아니라 서버 로직도 개발할 수 있어 생산성을 높임
 2. 논블로킹 방식으로 그림과 음악 파일들에 대해 효율적인 I/O 처리
 3. npm을 이용해 협업 시 버전 관리 용이

### [DB] **MongoDB**
 1. 프로젝트 초기 단계에는 완벽하게 DB 구조를 설계할 수 없다고 판단
 2. MongoDB는 noSQL 방식으로써, 개발을 하면서 필요한 필드를 유연하게 추가할 수 있어 빠른 개발에 적합
 3. 다른 noSQL DB보다 진입장벽이 낮음

<br>

## 시스템 구조

<br>

<p align="center"><img src="https://user-images.githubusercontent.com/37368480/117549622-6e69f780-b076-11eb-90ce-b1fb02976b48.png"></p>
 
<br>

- Web Server: React를 이용해 SPA 방식으로 끊김 없이 이야기를 즐길 수 있게 함. NginX를 이용하여 정적 웹 및 리버스 프록시 서버 구축
- API Server: Node.js를 이용하여 API 서버 구축. redis는 유저 정보 저장 용도로 사용
- Socket Server: socket broadcasting을 이용하여 선택지의 개수를 제한하면서 이를 실시간으로 렌더링 해주기 위해 지역변수 서버 활용
- Storage: 이야기 제작을 위해 사용자가 업로드한 오디오, 이미지 파일을 저장. 해당 파일들은 이후 이야기를 플레이할 때 불러오게 됨
- Database: 유저 데이터, 이야기 데이터 DB에 저장

<br>

## 주요 기능 소개

#### 이야기 탐험

- 여러 사람들이 만들어 놓은 이야기들을 즐길 수 있습니다.
- 선택지를 골라 자신이 원하는 이야기로 진행할 수 있으며, 미니맵을 통해 되돌아갈 수 있습니다.
 
<br>

<p align="center"><img src="https://user-images.githubusercontent.com/66366941/117540719-6ba5dd00-b04b-11eb-8a9e-100094ef51ec.gif"></p>
 
<br>


#### 이야기 이어나가기

- 이야기를 즐기다가 자신이 원하는 선택지가 없으면, 자신만의 이야기를 새로 만들어나갈 수 있습니다. 
- 게임에 추가되어 있는 사진과 음악들을 활용해 쉽고 빠르게 상상을 실제로 만들어낼 수 있습니다.
 
<br>

<p align="center"><img src="https://user-images.githubusercontent.com/66366941/117542299-09e97100-b053-11eb-8043-1c1b079df855.gif"></p>
 
<br>


#### 선태지 개수 동기화

- 이야기가 깊이 전개되도록 하기 위해서 선택지의 개수를 4개로 제한했습니다. 
- 선택지 개수가 1개 남은 상황에서 서로 다른 두 유저가 동시에 해당 선택지에 이야기를 이으려 한다면, 두 유저가 정성들여 만든 작품 중 하나는 사라지게 됩니다. 선택지의 개수를 실시간으로 동기화시켜 제작할 수 없는 선택지를 유저가 제작하게되는 일을 사전에 방지했습니다.
 
<br>

<p align="center"><img src="https://user-images.githubusercontent.com/66366941/117541839-c7bf3000-b050-11eb-9027-aa3819315d18.gif"></p>
 
<br>


#### 이야기 제작

- 다른 사람의 세계관에 내 이야기를 이어나가는 것이 아닌 자신만의 세계관을 펼쳐볼 수 있습니다.
- 이야기를 이어나가는데 사용될 사진과 음악들을 추가하고, 손쉽게 이야기를 세상 밖으로 내보내세요.
 
<br>

<p align="center"><img src="https://user-images.githubusercontent.com/66366941/117543011-ea077c80-b055-11eb-9cb7-d5958f6c03d6.gif"></p>

<br>

<p align="center"><img src="https://user-images.githubusercontent.com/66366941/117543397-9c8c0f00-b057-11eb-81d7-fde602492882.gif"></p>

<br>


##### 이야기 버전 추가

- 이야기는 처음부터 새로 만들고 싶지만, 사진과 음악들을 준비하기 귀찮은 분들을 위해 버전 추가하기 기능을 마련했습니다.
- 마음에 드는 사진과 음악들이 있는 게임에서 버전 추가하기 버튼을 눌러 진해할 수 있습니다. 버전 추가하기는 선택한 게임의 음악과 사진을 상속받습니다.

<p align="center"><img  width="300" src="https://user-images.githubusercontent.com/66366941/117543623-94809f00-b058-11eb-9442-7b96bed979e3.png"></p>










<br>

## 유저 피드백과 개선 사항
유저의 의견을 적극 구하고, 반영하는 등 유저를 만나기 위한 노력을 기울이고 있습니다.
(구글 애널리틱스, 카카오 로그인, 피드벡 메일)

#### 1차 배포 (2020.03.30)
- 랜딩, 게임디테일, 게임플레이, 프로필 등 기본적인 페이지 구현
- 스토리 리소스 생성, 스토리 플레이, 스토리 이어가기 등 필수적인 기능 구현
- 피드백
-> 서비스 컨셉에 대한 이해가 어려움
-> 스토리 수정에 대한 필요성

#### 2차 업데이트 (2020.04.12)
- 제작화면 개선
- 모바일 반응형 지원 
- Fork 기능 추가
- 비회원 플레이와 카카오 로그인 추가 (회원가입시 진행상황 보존)
- 서비스 이해를 돕기 위한 기능 추가
(참여자 수 표시, 기여자 랭킹, 프로필에 기여한 작품표시, 랜딩페이지 베너)
![image](https://user-images.githubusercontent.com/73219421/117559477-ae55cc80-b0c0-11eb-9b82-fa6737032864.png)
![image](https://user-images.githubusercontent.com/73219421/117559491-c75e7d80-b0c0-11eb-9a07-b50cc307d90f.png)
![image](https://user-images.githubusercontent.com/73219421/117559498-da714d80-b0c0-11eb-80d5-8298fb450c1e.png)
- 스토리 관리를 위한 기능 추가   
(트리 형태로 스토리를 디스플레이, 신고 수 파악을 통한 스토리 관리 기능)
<p align="center"><img  width="300" src="https://user-images.githubusercontent.com/73219421/117559545-30de8c00-b0c1-11eb-8466-3cdcd0ccce9a.png"></p>
- 유저 유입의 증가로 발전 가능성을 확인. 가장 많은 유입 경로는 op.gg로 저연령층에게서 큰 호흥을 얻음.
<p align="center"><img  width="300" src="https://user-images.githubusercontent.com/73219421/117559577-7733eb00-b0c1-11eb-8023-cf3899f842b0.png"></p>
- 피드백
-> ios 환경에서의 이슈
-> 스토리 
-> 스토리를 생성하기 불편한 진입장벽
-> 다양한 컨텐츠에 대한 피드백

<br>

## 개인 별 대표적인 기능 구현

#### 강민규: 진행상황 저장 기능

기능 설명: 컨텐츠의 길이가 길어진 상황에서는 사용자가 계속해서 첫 장면부터 다시 시작하기 보단, 진행중이던 장면에서 다시 시작하는게 맞다고 생각하여, 진행상황을 저장하는 기능을 만들었습니다.

구현 시 난관: 기능 구현 자체는 간단했습니다. 그러나 해당 기능을 구현하는 데 있어 엣지 케이스가 너무 많았습니다. 간단하게 사용자 모덷에 진행상황 필드를 추가하면 구현은 가능하지만, 사용자가 갑자기 진행방향에 어긋나는 장면에 들어간다던지 하는 경우, 진행 상황이 흐름에 맞지 않게 저장되는 문제가 있었습니다. 

해결 방법: 유효성을 검증하는 방식으로 검증되지 않은 장면으로는 접근하지 못하도록 막았습니다. 

#### 조성현: 랜딩 페이지

기능 설명: 서비스를 처음 방문해서 사용자가 어떤 서비스인지 인지할 수 있도록 하는 화면을 고민했습니다. 어도비 등의 사이트를 참고해 서비스 모토와 설명을 담은 베너를 가장 잘 보이게 만들었습니다. 넷플릭스를 참고하여 컨텐츠 중심의 레이아웃을 만들었습니다.

구현 시 난관: 모바일, 웹의 다양한 화면크기에서도 빈 화면이 없도록 하고 컨텐츠가 보기 좋은 크기를 갖도록 해야했습니다. 

해결 방법: 미디어 쿼리와 이벤트를 사용해 현재 화면 사이즈에 대응하도록 반응형으로 만들었습니다. 컴포넌트화를 통해 손쉽게 베너와 컨텐츠들을 추가해 디스플레이 할 수 있습니다.

#### 김승현: 제작 페이지

기능 설명: 이어봐는 사용자가 플레이하는 것뿐만 아니라 릴레이로 이야기를 이어나가는 플랫폼이기에 이야기를 제작할 수 있는 툴이 필요합니다. 해당 페이지에서 에셋을 업로드하는 기능과 유저가 편리하게 제작할 수 있도록 UI/UX를 구상하고 구현하였습니다.

구현 시 난관: 이어봐에는 인물 이미지, 배경 이미지, 배경음, 효과음으로 4가지 범주의 에셋이 존재합니다. 이때 _1. 사용자 편의성을 위해 임의의 순서로 에셋들을 업로드할 수 있도록 지원해 줘야 했습니다._ 또한 _2. 스토리지 부하 및 API 요청을 줄이기 위해 업로드한 파일들을 즉시 서버에 전송하지 않고, 사용자가 파일이 의도한 대로 잘 올라갔는지 확인할 수 있도록 렌더링 하여 주다가 이를 확정 지었을 때에만 서버에 보내야 했습니다._

해결 방법: 첫 번째 상황을 처리하기 위해 이야기DB를 깊은 복사한 임시 데이터에 새로운 파일들을 반영하여 렌더링 해주었습니다. 두 번째 상황은 유저가 업로드를 확정 지었을 때 파일들을 분류하여 이야기DB에 한 번에 반영해 주는 방식으로 해결하였습니다.

<br>

## 추가로 구현하는 중인 & 기획중인 기능

#### 1) 에셋 스토어

* 사용자들이 최초의 이야기를 만들어 내기에 어려움이 있다는 피드백을 반영하여, 모든 사용자에게 제공되는 에셋 스토어 기능을 구현 중입니다
* 주인공, 배경사진, 배경음악, 효과음들이 제공될 예정입니다.
* 현재 기능은 구현완료하였으며, UI/UX 작업 중에 있습니다

#### 2) 이야기 삭제

* 이야기가 진행됨에 있어서 이후의 이야기들에 영향을 미칠 수 있기 때문에 초기 버전에는 삭제를 따로 구현하지 않았습니다.
* 하지만, 컨텐츠의 퀄리티를 저해할 수 있는 이야기들이 중간에 추가될 수 있다는 판단 하에 이야기 삭제 기능을 검토 중입니다.
* 이야기 트리, 리소스 관리 부분에도 영향을 끼치기 때문에 계속해서 논의 중에 있습니다.

#### 3) 리소스 삭제

* 이야기에 사용되는 사진, 음악 파일들이 계속해서 S3 스토리지에 축적되고 있습니다.
* 이를 방지하기 위해 사용하지 않는 파일들을 제거하기 위해서 reference count 를 이용한 로직을 활용할 예정입니다.
* 추가로 이야기 별로 파일들을 저장하여 관리에 용이하게 변경시킬 예정입니다.

#### 4) 스토리 추가 시 알림

* 본인이 만든 이야기에 누군가 이어서 제작했다면, 알림을 전송하는 기능을 제작 중입니다.

#### 5) 작성자 초대 모드

* 본인이 작성한 이야기에 익명의 사람들이 무분별하게 추가하는 것에 불편함을 느끼는 유저들이 존재한다는 피드백을 받았습니다.
* 이러한 분들을 위해, 본인이 초대한 작성자에 한해서 이야기를 이어나갈 수 있는 모드 제작 예정 중입니다.
* 아무도 초대하지 않을 경우, 본인만 작성할 수 있는 기능입니다.



