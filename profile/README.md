# 🎙️ 실시간 채팅 애플리케이션 🎧
빽(Backend)없고 뒤(Design)없는 프론트엔드 4명의 풀스택 개발  
<br />  

<hr />
<div style="display: flex; justify-content: center; align-items: center; ">
  <img src="https://github.com/Codeit-part4-team3/pq-client/assets/68732996/15a7ead1-1adc-4208-9869-104de9cb0ad8" width="400" />
  <img src="https://github.com/Codeit-part4-team3/pq-client/assets/68732996/9292ff9d-19cf-413c-911d-823d1c67e36a" width="400" />
  <img src="https://github.com/Codeit-part4-team3/.github/assets/68732996/cf0586c6-c707-4215-a1a9-5e9320d7e4f3" width="800" />
  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbrB10K%2FbtsGVLT8WUY%2FdvKJ14eCKkyIzmZpaeusu1%2Fimg.png" width="800" />
</div>

<hr />
<br />

## 🪄 Skill
React, Express, NestJS, Prisma(MySQL) AWS  
<br />

## 📱 주요기능
- 회원가입(OAuth) 및 로그인
- 실시간 채팅(음성/화상 포함)
- 멤버십 결제
<br />

## 🔥 핵심 개발내용
- AWS Route53/CloudFront/S3로 프론트엔드(React) 배포 및 이미지 저장
- MSA 서버구조(유저, 채팅, 소켓)로 AWS EC2에 배포(private)
    - 서버별 DB분리 유저/채팅서버(mysql), 채팅메시지(dynamoDB)
- AWS Cognito를 사용하여 유저관리(구글, 카카오 회원가입)
- Socket을 이용한 채팅 기능 구현
- WebRTC를 활용하여 p2p기반의 N:M 음성/화상 스트림 통신 구현
- WebSocket을 통한 실시간 통신 구현
  - 서버:체널=1:N 구조로 Room을 통한 socket 관리
- Web Speech API를 이용해서 음성 입력을 텍스트로 변환 하는 회의록 기능 구현
- 토스페이먼츠 SDK를 사용한 결제 시스템 구현 
- CI/CD 구축
    - Jest를 활용하여 PR시 테스트 자동화
    - Git Actions와 AWS Codedeploy를 사용한 자동배포
<br />

## 서버 별 내용

### 👩‍💼👨‍💼 유저서버
#### 기술 스택
  - NestJs와 Prisma를 사용해서 빠르게 개발 진행
  - AWS Cognito와 별도의 userdb를 병행 사용해 유저 관리와 토큰 관리를 효율적으로 진행
    
#### 주요 기능 및 설계
  - JwtAuthGuard: 특정 API는 토큰이 없을 경우 예외 처리하여 접근 제한
  - AdminGuard: 관리자 전용 API 접근을 AWS Cognito custom role로 관리
    
  - OAuth 로그인/회원가입: 동일 이메일 사용 시 OAuth를 통한 로그인 및 회원가입 지원으로 유저 사용감 개선
  - 유저 프로필 이미지 관리: 유저가 업로드한 이미지 파일을 S3에 저장하고, 반환된 URL로 DB를 업데이트  
  - 결제 및 환불: 토스페이먼츠 SDK를 이용한 결제 처리 및 환불 관리
  - 구독 및 플랜: 유저의 구독 생성과 갱신 및 취소, 플랜 관리
  - 이벤트: 관리자가 이벤트 시작 및 종료를 직접 조정, 결제 누적 금액 및 이벤트 참가자 관리
<br />

### ⌨ 채팅서버
#### 기술 스택
  - NestJS와 Prisma를 사용해서 빠르게 개발 진행

#### 주요 기능 및 설계
  - 서버, 체널 CRUD
  - 서버 링크로 초대/이메일로 초대 기능 구현
  - 채팅 메시지 알림
  - 채팅 메시지에 안읽은 사람 수 표시
  - 간단한 일정을 위해 시작 시간, 일정 이름, 서버 아이디로 간단한 db설계
  - 서버간 통신(httpservice)으로 유저정보에 서버 내 유저정보를 요청
<br />

### 🔊 소켓 서버
#### 기술 스택
  - express를 이용해서 서버 구현
  - AWS DynamoDB를 사용
    
#### 주요 기능 및 설계
  - DynamoDB 사용
  - Socket기반 채팅 메시지 CRUD 구현 및 회의록 작성 구현
  - WebRTC로 N:M 음성, 화상 채팅 구현

<br />
  
## 🎸기타 개발내용
- 서버 초대 기능(이메일 초대, 초대링크(암호화))
- 개별 스트림 통신(음성, 화상) 제어기능 구현
- 디버깅 & 모니터링을 위해 서버별 로그 수준별로 저장
- 팀원 모두 SQL에 대한 숙련도가 부족한 상황에서 빠른 개발을 위해 Prisma(ORM)을 사용
- 서버별 일정 기능 구현
- 실시간 토스트 기능 구현
- 멤버 정보 10초 단위로 업데이트
- 스웨거 생성 경험

<br />  
  
## 기타 개발 이미지
<img src="https://github.com/Codeit-part4-team3/pq-client/assets/59861974/2dae6a46-a03b-4b99-8d3a-afe325a69be8" width="400" />
<img src="https://github.com/Codeit-part4-team3/pq-client/assets/59861974/938188b5-de7d-4216-bd96-306d691770db" width="400" />  
<img src="https://github.com/Codeit-part4-team3/.github/assets/98401099/aabf7adc-feec-4f77-b607-61739418bf16" width="800" />


<br />    
<br />  

## 아쉬웠던 점
- 테라폼(Infrastructure as code)을 도입하여 인프라를 코드로 형상관리하려 하였으나, 개발 딜레이로 초기 EC2관련 리소스스 설정에 그친것이 아쉬웠다. 이후 추가개발과 AWS아키텍쳐 자격증 준비와 동시에 Terraform으로 현재 인프라 구조를 설정하고 이후 관리할 예정이다.
- 친구 목록 db를 설계는 했지만, 시간이 부족하여 기능을 추가하진 못했다.
- API gateway를 통해 클라이언트 요청과 라우팅 관리를 하려 하였으나 여러 이슈에 대한 정보가 부족한 상태에서 개발일정도 고려해야 했기에 과감히 제외하는 선택을 했다. 이후 AWS에 대해 추가로 학습하며 다뤄볼 예정이다.
- N:M 음성, 화상 채팅의 경우 맨처음엔 SFU방식으로 구현할 예정이였지만 알 수 없는 이슈로 지지부진하다가 시간이 촉박해서 P2P방식으로 변경해서 구현함. 이후 SFU방식으로 바꿔나갈 예정 
<br />  
  
## ❗ 이슈 및 해결
### ❓ [MSA 서버구조의 로컬환경] 로컬환경에서 개발 및 테스트 시 유저서버와 채팅서버가 동일한 포트번호를 사용하고 있는 문제 발생. Port번호를 다르게 한다면 서버별로 API URL을 구분해야함
API 요청 시 axios instance를 사용하고 있음 -> BaseURL을 구분해주면 어떨까<br />
서버별로 axios instance를 만들수도 있으나 추후 서버가 늘어나거나 api의 갯수가 늘어나면 휴먼에러가 빈번해질 수 있는 문제<br />
> <strong>😎</strong>
> <strong>로컬전용 프록시서버를 만들어서 경로기반 라우팅을 적용하여 해결</strong>
<br />

### ❓[React + Socket] Socket통신중 채팅창 페이지에서는 채팅메시지 알림 이벤트를 처리가능한데 다른 특정 페이지에서 알림 이벤트를 처리 불가한 현상
> <strong>😎</strong>
> <strong> useSocket훅을 만들어서 프로그램 내에서 단 하나의 소켓인스턴스를 관리<br /></strong>
> <strong> 각 컴포넌트들에서는 socket.on으로 처리되는 각 메서드들에 대한 핸들러 함수만 관리하는 구조로 변경<br /></strong>
<br />  

### ❓[???] AWS S3에 upload하는 동작이 한명의 컴퓨터에서만 에러를 일으키는 현상
코드를 다시 clone해보고 동일한 .env파일 내용을 적용했으나 에러는 동일
계정문제인가 싶어서 정상인 컴퓨터에서 문제됬던 계정으로 시도하니 정상동작함 / 문제있는 컴퓨터에서 성공했던 계정으로 시도하니 실패
이것저것 시도해보고 리서치해보다가 환경변수에 로그를 찍어보라고 하여 보니 .env파일의 환경변수와 다른 값임... ?!?!??<br />
> <strong>😎</strong>
> <strong> 컴퓨터의 시스템환경변수에 가보니 .env파일과 동일한 이름의 키값이 존재했음<br /></strong>
> <strong> 이전에 테라폼 설정을 하면서 시스템 환경변수에 AWS관련 키를 추가했는데 공교롭게도 이름이 똑같아서 발생한 문제였다.<br /></strong>  
<br />

### ❓[EC2 + Nest] AWS EC2 Heap메모리 부족현상 발생
> <strong>😎</strong>
> <strong> aws-sdk 전체를 임포트 하니 메모리 부족 <br /></strong>
> <strong> aws-sdk 내부에서 필요한 부분만 임포트 하여 해결 <br /></strong>
<br />

### ❓[토스페이먼츠 SDK] 결제 승인 요청 중 accessToken 재발급 과정에서 최종적으로 요청은 성공하지만 첫 401 에러를 결제 실패로 인식하는 현상
> <strong>😎</strong>
> <strong> 결제 승인 요청을 마운트 후 바로 진행하지 않고, 모든 상태가 업데이트 된 후에 결제가 진행되록 설정<br /></strong>
> <strong> <br /></strong>  
<br />

### ❓[JWT] refreshToken Cookie에 저장 후 httpOnly 옵션 활성화 시 서버로 전송 불가 이슈
> <strong>😎</strong>
> <strong> 모든 api 요청은 `api.pqsoft.net`으로 보내도록 설정했기에 `domain: 'pqsoft.net'`옵션 추가로 메인 도메인 및 하위 도메인 쿠키 접근 하용 설정으로 해결<br /></strong>
> <strong> <br /></strong>  
<br />

### ❓[WebRTC] AWS 배포 후 WEBRTC 시그널링 과정이 안되는 이슈
STUN서버를 사용하는 상태에서는 AWS 내부의 방화벽 등의 여러가지 장벽 떄문에 피어 연결이 불가능한 이슈가 발생함.
> <strong>😎</strong>
> <strong> EC2 인스턴스를 하나 사용해서 coturn 라이브러리를 이용해 turn서버를 구현했음. <br /></strong>
> <strong> <br /></strong>

### ❓[AWS DynamoDB] 테이블의 파티션 키와 정렬 키가 아닌 속성으로 쿼리 요청 불가능한 이슈
채팅 메시지 수정, 삭제 기능 구현 중 채팅 메시지의 파티션 키가 channelId이고 정렬 키가 createdAt이였음. 
messageId 속성으로는 해당 메시지에 접근이 불가능한 이슈가 발생함
> <strong>😎</strong>
> <strong> DynamoDB의 Global Secondary Indexes(GSI)를 이용해서, 파티션 키와 정렬 키가 아닌 속성을 파티션 키 또는 정렬 키로 하는 테이블 생성가능 <br /></strong>
> <strong> <br /></strong>

### ❓[Web Speech API] 클로바, 구글 STT 등 음성 인식 라이브러리 비용 이슈
무료 상태로 개발을 끝내기가 불가능 하다고 판단을 해서 비용 이슈가 발생.
> <strong>😎</strong>
> <strong> Web API인 Web Speech API를 이용해서 음성 입력을 텍스트로 변환한 회의록 기능 구현함. <br /></strong>
> <strong> <br /></strong>
<br />
