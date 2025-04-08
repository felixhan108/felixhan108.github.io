---
title: Backend 기초지식식
version: "0.0.1"
latestUpdate: "2025-04-08"
description: 웹서버를 만들기 위한 기초지식을 정리해 보았습니다.
---

## 백엔드 JOB 포지션

- 서버 개발
- 데이터베이스 설계 및 관리
- API 개발
- 보안 및 인프라 관리
- 네트워크 설정

## 기본지식

### 네트워크

> 좀 더 깊이 있게 공부하고 싶다면 다음 키워드를 검색

- 내부 IP, 외부 IP
- 유동 IP, 고정 IP
- DNS, hots 파일
- 레스트리, 레스트라
- well-konwn port, registred prot, dynamic port
- 포트 포워딩
- OSI 7계층, TCP/IP 4계층

### 운영체제

> 운영체제의 주요 기능

- 프로세스 관리
- 메모리 관리
- 파일 시스템 관리
- 네트워크 관리

> DeepDive

- 뮤텍스
- 세마포어
- 데드록
- 기아 현상
- 식사하는 철학자 문제
- 피터슨 알고리즘
- CPU 스케주링 알고리즘 : FCFS, SJF, SRF, RR

### 데이터베이스

entity : 명사 -> 회원
attribute : 명사 안에 있는 속성 -> 회원번호,이름,나이 등..
relation : 저장 단위 -> 표

- tuple : 행단위 데이터
- domain : 각 속성이 가질 수 있는 값의 집합 예) 이름 속성의 도메인은 {2~10글자 문자열}
- key : 테이블 내 속성 간의 관계와 테이블 간의 관계
  - 슈퍼키
  - 후보키
  - 대체키
  - 기본키 : 중복X, 최소1개 (예 : 회원번호)
  - 외래키 : 테이블간의 관계를 나타내는 키 (예 : 주문 테이블에서 사용된 '회원번호'는 회원 테이블의 기본 키 이다. )

### 자료구조

> [!note] 시간복잡도
>
> - O(1) : 각각의 요소를 탐색하는 시간
> - O(log n) : 로그 시간 복잡도 : 요소 수가 많아져도 비교적 시간 상승폭이 완만함
> - O(n) : 선형 시간 복잡도 : 입력되는 요소 수에 비례
> - O(n2) : 제곱 시간 복잡도 : 입력되는 요소 수의 제곱에 비례해 시간이 걸립니다.

#### 배열 : Array[]

> 배열은 삽입 하거나 삭제 하는 방식 보단 '탐색'의 비중이 높은 경우 많이 사용됩니다.

#### 연결 리스트 : linked-list

> [!note] 캐러셀 또는 슬라이드 구현
> 큰 데이터셋의 효율적인 삽입/삭제가 필요한 경우

> 삽입 또는 삭제에 걸리는 시간이 O(1)로 빠른 편
> 탐색 시간은 O(n)이 소요 됩니다.

#### 스택

> [!note] 브라우저의 뒤로 가기 / 앞으로 가기
> 실행 취소/다시 실행 기능
> 깊이 우선 탐색 (DFS) 알고리즘을 사용하는 경우 (복잡한 트리 구조 탐색)

> 바구니 방식 들어오는 순서와 나가는 순서가 다름

#### 큐

> 들어온 순서대로 나가는 방식

#### 그래프 : graph

> [!note] 소셜 네트워크 관계표현, 내비게이션 시스템이나 경로 찾기 알고리즘 구현

> vertex 와 edge(간선)으로 이루어짐

#### 트리 : tree

> 계층적 데이터의 집합 : dom html은 tree 구조임

#### 맵 : map

> 키-값(key-value) 쌍으로 이뤄진 데이터의 집합 : Object, NoSql 이 이 형식임.

#### Deep Dive

- 선형 자료구조, 비선형 자료구조
- 해시 테이블
- 이진 트리
- 이진 검색 트리
- 힙
- 우선수위 큐

### 객체지향

> [!note] javascript의 api
> 대부분 객체지향으로 작성되어 있어 구조를 이해하기가 편하다.

#### 추상화

class 정의

#### 캡슐화

속성과 그 속성을 조작하는 기능(함수)를 하나의 '캡슐'로 묶는 것을 말함.
외부로 노출하고 싶은 속성이나 기능을 제어하기 위함

#### 상속

기존 기능에서 새로운거 하나가 특별하게 추가되야 할때 적용 하는 방식

### 함수형 프로그래밍

#### 불변성

immutability : 데이터는 일단 생성되면 변하지 않아야 한다.
겉보기에는 불편하게 여겨질 수 있으나 아래와 같은 장점이 있다.

- 어떤 변수가 예상치 못한 상황에서 엉뚱한 값으로 바뀔 가능성이 있음.
- 자신이 작성한 프로그램이 어떻게 동작할지 예측하고 프로그래밍할 수 있음.

#### 선언형

==무엇을 어떻게 할 것인지== -> =='무엇이 할 것인지'== 에 초점을 둡니다.

## DBMS

### RDBMS - 관계형 데이터 베이스

> [!note] RDBMS 종류
> Oracle, MySQL, PostgreSQL, MariaDB

#### 회원 테이블

| 회원번호 | 이메일           | 비밀번호 | 이름   | 나이 |
| -------- | ---------------- | -------- | ------ | ---- |
| 1        | thepub@gmail.com | abc@#$   | 김찰스 | 20   |
| 2        | thepub@gmail.com | 22       | 한수철 | 33   |

#### SQL (Structured Query Language)

```sql
/* User 데이터에서 30 살보다 크거나 같은 사람을 찾아줘 */
SELECT * FROM User WHERE age >= 30;
```

### NoSQL - SQL을 사용하지 않는 DBMS

RDBMS로 관리하기에 적합하지 않은 데이터입니다.
저장 형식이 일정하지 않은 비정형 데이터를 효율적으로 관리하기 위해 개발 되었습니다.

> [!note] 저장유형
> 도큐먼트데이터베이스, 키-값 데이터베이스, 그래프 데이터베이스

### CRUD

##### RDBMS에서의 CRUD

##### user

| id  | email | password | name | age |
| --- | ----- | -------- | ---- | --- |

##### order

| id  | userId | productId | count | adress | orderDate |
| --- | ------ | --------- | ----- | ------ | --------- |

##### porudct

| id  | name | stockQuantity | price |
| --- | ---- | ------------- | ----- |

#### 테이블 생성

CREATE 문을 실행하면 데이터가 저장되지 않은 빈 user 테이블이 생성 됩니다.

```SQL
CREATE TABLE user (
	id BIGINT NOT NULL AUTO_INCREMENT,
	email VARCHAR(320) NOT NULL,
	password VARCHAR(500) NOT NULL,
	name VARCHAR(45) NOT NULL,
	age INT NULL,
	PRIMARY KEY (id)
);

CREATE TABLE order (
	id BIGINT NOT NULL AUTO_INCREMENT,
	userId BIGINT NOT NULL,
	productId BIGINT NOT NULL,
	count INT NOT NULL,
	adress VARCHAR(100) NOT NULL,
	orderDate TIMESTAMP NOT NULL,
	PRIMARY KEY (id)
);

CREATE TABLE product (
	id BIGINT NOT NULL AUTO_INCREMENT,
	name VARCHAR(100) NOT NULL,
	stockQuantity INT NULL,
	price INT NULL,
	PRIMARY KEY (id)
);
```

#### 데이터 생성

```SQL
INSERT INTO user(email, password, name, age)
VALUES('abc@gamil.com', 'abc@@@', '한성수', 36);
```

#### 데이터 조회하기

```SQL
SELECT * FROM user;
```

#### 데이터 수정하기

```SQL
/* 비밀번호 수정 */
UPDATE user SET password = 'abcd@#$@#$' WHERE name = '홍성수';
/* 결과확인 */
SELECT * FROM user;
```

#### 데이터 삭제하기

```SQL
DELETE FROM user WHERE name = '한성수';

SELECT * FROM user;
```

#### 테이블 조인

```SQL
/* user 테이블의 id 와 order 테이블의 userID 가 같은 것을 연결 */
SELECT * FROM user INNER JOIN order ON user.id = order.userId;
```

### NoSQL

table = collection
tuple = document (filed-value)

- 데이터베이스\_1
  - 컬렉션\_1
    - 도큐먼트\_1
    - 도큐먼트\_2
    - 도큐먼트\_3
  - 컬렉션\_2

## API

### API 개발 순서

1. 엔드포인트 설계
2. HTTP 매서드 지정
3. 데이터 포맷 및 프로토콜 선택
4. 엔드포인트 구현
5. 인증 및 보안
6. 오류 및 예외 처리
7. 테스트와 디버깅
8. API 문서화

#### 1. 엔드포인트 설계

/search, /curation 등을 결정함.

#### 2.HTTP 메서드지정

POST, GET, PUT or PATCH, DELETE

#### 3. 데이터 포맷 및 프로토콜 선택

데이터 포맷 : JSON, 프로토콜 : RESTful

#### 4. 엔드포인트 구현

클라이언트의 요청을 받으면 데이터베이스에 접근해 데이터를 가져와 가공하고, 이를 클라이언트에 반환하는 프로그램 로직을 만듬.

#### 5. 인증 및 보안

API를 보호하기 위해 인증 및 보안 메커니즘을 구현합니다.

- 사용자 인증
- 액세스 토큰 기반의 권한 부여
- 암호화 등

#### 오류 및 예외처리

잘못된 요청이나 예외 상황에 대해 적절한 오류 응답을 할 수 있도록 프로그램 로직을 보강

#### 테스트와 디버깅

테스트와 디버깅 단계를 거쳐야 함, 그럼으로써 API의 정확성,안정성 등등..

#### API 문서화

앤드포인트, 매개변수, 응답 형식, 오류코드 등에 대한 명세를 문서로 작성

### REST API

웹의 장점을 활용해 만든 API 설계 스타일

#### 자원

서버가 주고받는 자원을 URI로 명시를 함.
http://www.test.com/users/100

```scheme
scheme:[//[user[:passowrd]@]hots[:port][/path][?query][#fragment]]
```

#### 행위

CRUD 행위를 표현함
/delete/users/1

```scheme
GET /users/:id
POST /users
PATCH /users/:id
DELETE /users/:id
```

#### 표현

### GraphQL

## 클라우드 컴퓨팅

AWS의 각종 서비스를 알아 봅니다.

### 서버 종류

#### EC2

가상 컴퓨터 : 운영체제를 선택하고 서버를 운영할 수 있습니다.
사용예 : 웹서버, API 서버, 프록시 서버, FTP 서버

#### S3

파일 저장 스토리지 : 파일을 넣고 꺼낼때 비용이 듬
사용 예 : 웹사이트 호스팅, 미디어 콘텐츠 호스팅, 데이터 백업 및 복원, 데이터 저장 및 분석

#### RDS

데이터베이스 시스템 : 제공하는 시스템 - MySQL, PostgreSQL, Oracle등
기능 : 데이터베이스 생성, 백업 & 복원, 모니터링, 자원 자동 조정

#### IAM

AWS 자원에 접근하고 사용할 수 있는 사용자 권한을 제어합니다.
기능 : 사용자 권한 관리, 사용자 역활 관리, 사용자 그룹 관리, 자원 정책 접근 관리, 암호 정책, MFA 관리(MFA: Multi-Factor Authentication : 인증 요소를 사용하는 보안 매커니즘)

### 온프레미스 시스템

1. 애플리케이션
2. 데이터
3. 런타임
4. 미들웨어
5. 운영체제
6. 가상화
7. 서버
8. 스토리지
9. 네트워크

### IaaS

> 대표적인 시스템 : AWS, AZURE, GCP

1. 애플리케이션
2. 데이터
3. 런타임
4. 미들웨어
5. 운영체제

### PaaS

> 대표적인 시스템 : Heroku, Google App Engine, Azure App Service

1. 애플리케이션
2. 데이터

### SaaS

> 대표적인 시스템 : Saleforce, Google Workspace, Microsoft365

1. 전부다 제공해줌

## 가상화와 컨테이너

> 가상화(Virturalization)란?
> 하나의 물리적인 서버를 여러대 처럼 사용하는 기법

### 도커

#### 도커구조

도커 클라이언트 -> 도커 호스트 -> 도커 데몬 -> 도커 이미지 -> 컨테이너 실행

- 도커 클라이언트 : cli로 도커에게 명령합니다.
  - docker build
  - docker pull
  - docker run
  - ...

#### 도커 허브

Hub.docker.com
도커의 허브 (온라인 도커 저장소)

#### 도커 이미지

도커 파일에 텍스트로 만드는 파일

#### 컨테이너 실행과정

1. 도커 실행
2. 도커 데몬 실행
3. 도커 이미지 find
   - 로컬
   - 도커 허브 : 이미지가 없는 경우
4. 새로운 컨테이너 생성 및 실행
5. 명령 실행 완료 후 컨테이너 종료

### 컨테이너 오케스트레이션

서버 클러스터(여러서버를 하나의 시스템으로 묶은것) 에서 다수의 컨테이너를 관리하기 위해 나옴

#### kubernetes (k8s)

전체적인 도커를 관리할 수 있는 거시기

## 웹 애플리케이션 아키텍쳐

### 모놀리식 아키텍쳐

단 방향 전체 아키텍쳐
모든 서버가 1개로 이루어 져있다고 보면된다.
사용자 -> 클라이언트 -> 서버 -> 데이터베이스(게시글,동영상,이미지)

### 마이크로서비스 아키텍쳐

사용자 -> API 게이트웨이 -> 게시글(1), 이미지(1), 동영상(1)

### 서버리스 아키텍쳐

개발자가 서버를 신경쓰지 않고 개발하는 영역

#### BaaS(Backend as a Service)

- firebase
- suapbase
- AWS AppSync
- Azure Cosmos DB

#### FaaS(Function as a Service)

## 테스트와 CI/CD

ci/cd는 aws 로 운영할때 어떤식으로 작업할 수 있는지 github Action과 aws의 연계를 한번 해봅니다.

### 테스트

#### V Model

1. 요구 사항 분석
2. 시스템 설계
3. 상세 설계
4. 구현
5. 단위 테스트
6. 통합 테스트
7. 시스템 테스트
8. 인수 테스트

#### 테스트 주도 개발(DDD, Test-Drvien Development)

- 빨강 : 개발 후 테스트할 영역을 미리 짜둔다.
- 초록 : 초록색으로 바꿔가며 개발을 한다.
- 리팩터링 : 초록색을 확인하며 리팩토링을 한다.

### CI/CD

> Continuous Integration / Continuous Delivery or Deploment (지속적 통합 / 지속적 배포)

#### flow

##### CI (지속적 통합)

1. coding
2. build
3. test

##### CD (지속적 배포)

1. test
2. release
3. deploy

#### CI 도구

- 젠킨스
- 깃허브 액션
- 트래비스 CI
- 서클 CI

#### CD 도구

- AWS 코드디플로이

#### 통상적인 구조

> Jenkins || Github Actions -> AWS CodeDeploy
