# Hyperledger-network

## 개발배경 및 목적
블록체인은 개인 간 거래 정보를 중앙 서버가 아닌 모든 참가자들의 네트워크에 공유 하는 ‘분산형 디지털 장부’ 기술이다.
이 기술은 거래 정보를 암호화된 개별 블록으로 체인형식으로 엮어 모든 참가자들에게 저장하는 방식이다.
이런 특징을 갖고 있어 블록체인은 해커와 같은 악의적인 유저가 한 블록에 침투하더라도 나머지 블록 모두 위변조하기가 어려워 보안 측면에서 주목을 받고 본인인증 시에 많이 쓰이고 있다.
또, 요즘 자신 명의의 핸드폰 속 앱을 이용한 신원인증이다. 하지만 하드웨어에 정보가 저장되어 있어 높은 하드웨어 의존성을 갖고있다. 사용자들의 지문과 같은 생체 정보를 블록체인 내부에 저장해 두고, 인증할 때마다 사용하면 아날로그 지갑의 필요성과 하드웨어의 의존성이 작아지고 보안에도 강한 본인인증이 가능할 것 같아 진행하게 됐다.


## 개발환경 및 개발언어
1. Go - 1.16.5 linux/amd64
2. Hyperledger Fabric Chaincode 
3. Finger print image compare  - Python 2.7, 3.7
4. Node - 12.22.10
5. Docker - 20.10.12
6. Docker Compose - 1.27.2

## 시스템 구성
![image](https://user-images.githubusercontent.com/76714219/190954793-6fc688dc-6f1c-4379-8eae-66621eef6f94.png)


## 프로젝트 주요 기능
![image](https://user-images.githubusercontent.com/76714219/190954950-3d1f7681-fbf6-4059-9f20-7c3044eb9412.png)

1. 회원가입
하이퍼 레저 페브릭(블록체인) 네트워크에 만들어서 배포된 체인코드(스마트 컨트랙)는 NoSQL DB에 원하는 DB를 빼오기 위한 고정맞춤 쿼리문을 배포하는 것과 같다. 앱에서 회원가입 할 사용자의 ID, 이름, 나이, 거주지, 지문 이미지 등을 받아오면 블록체인(DB) 내에 중복되지 않으면 회원가입 한다.

2. 로그인(신원인증)
서버는 앱에서 유저 ID와 지문 이미지를 받으면 블록체인 내 해당 ID의 지문이미지를 요청한다. 서버에서 앱에서 받은 로그인하려는 이미지와 블록체인에서 받은 회원가입 시의 이미지를 인공지능 모델로 비교한 후 일정 정확도 이상이 일치하면 해당 ID의 인증정보(현재는 성인인증여부)를 반환하고 일치하지 않으면 불일치 여부를 반환한다.


## 오픈소스 출처
https://github.com/hyperledger/fabric-samples

## 🚀 기능 목록
### app.js (apiserver)
- [x] port open to http request, response
- [x] route open
- [x] administrate request
### app.py (AI apiserver)
- [x] port open
- [x] get compare image
- [x] Image Pretreatment
    - [x] increase brightness
    - [x] image resize
    - [x] image color change to gray
    - [x] image const change
    - [x] image fillter with adaptive thresh gaussian
- [x] compare block chain fingerprint and appliciont fingerprint
### fabinfo.js (chaincode)
- [x] query to member sign up 
- [x] query to get fingerprint image
- [x] query to get memeber is adult or not
- [x] query to get memebr's school
### addInfo.js (Sign up)
- [x] receive sing up member information
- [x] if already member, get error response
- [x] check block chain permission user
- [x] execute query to member information save block chain
- [x] response sing up result
### queryFinger.js
- [x] check block chain permission user
- [x] execute query to get fingerprint image at block chain
- [x] save block chain image to server
### queryAuth.js
- [x] check block chain permission user
- [x] execute query to get member is audlt or not
- [x] response member age certification
### querySchool.js
- [x] check block chain permission user
- [x] execute query to get member's school
- [x] response member school certification
### upload.js (Log in)
- [x] check block chain permission user
- [x] receive user's fingerprint and member_id
- [x] get fingerprint image from block chain 
- [x] create request AI server to compare image
- [x] if user correct, after additional certification continue
- [x] if user uncorrect, create exception response
- [x] delete fingerprint images
- [x] response app certification result