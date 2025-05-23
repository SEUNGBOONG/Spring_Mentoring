#스프링 미션 안내

---

## 목차

1. [설명](#1-설명)
2. [규칙](#2-규칙)
3. [미션](#3-미션)

- [3-1. mission-racing](#3-1-mission-racing)
    - [미션 설명](#미션-설명)
    - [미션 내용](#미션-내용)
    - [API 문서](#api-문서)
        - [1. 자동차 이름 등록 (POST)](#1-자동차-이름-등록-post)
        - [2. 자동차 경주 시작 (POST)](#2-자동차-경주-시작-post)
        - [3. 자동차 경주 결과 조회 (GET)](#3-자동차-경주-결과-조회-get)
        - [4. 자동차 경주 결과 개별 조회 (GET)](#4-자동차-경주-결과-개별-조회-get)
- [3-2. mission-lotto](#3-2-mission-lotto)
    - [미션 설명](#미션-설명-1)
    - [미션 내용](#미션-내용-1)
- [3-3. mission-board](#3-3-mission-board)
    - [미션 설명](#미션-설명-2)

---

## 1. 설명
- Java 미션과 동일.
- 미션 시작시 Fork 및 클론을 한 후 `[미션명/step1, 미션명/step2]` 라는 브랜치 명으로 `두 단계 걸쳐 미션을 진행`합니다.
- 단계 별 완료 후 `` 레포지토리에 자신 깃허브 id에 해당하는 곳으로 pr을 올립니다.
- 미션 순서는 racing -> lotto -> board 순서입니다.

---

## 2. 규칙

- 미션 별로 `README.md 생성` 및 `기능 구현 목록과 고민한 점에 대해 작성`해서 제출해주세요.
- setter를 지양해주세요.
- 인덴트 2가 넘어가지 않도록 해주세요.
- 가급적 가능한 모든 메서드에 대해 테스트를 진행해주세요.
- 메서드의 기능 단위를 최대한 작게 유지해주세요.
- 불필요한 dependency 추가는 지양해주세요.
- 구글링은 좋으나 `gpt는 가급적 사용하지 말아주세요.`
- 자신이 작성한 코드가 어떤 역할을 하는지 최대한 이해하면서 미션을 진행해주세요.
- 미션 제출 전 불필요한 import, 주석을 모두 제거하고 정렬한 후 제출 해주세요.

---

## 3-1. mission-racing

### 미션 설명

- 스프링 API 서버를 만드는 연습을 합니다.
- 레이어드 아키텍처에 대해 학습합니다.
- 구조적으로 유연하게 생각하며 콘솔과 API 서버를 모두 실행할 수 있게 만듭니다.
- 기본적인 스프링의 동작 원리를 파악합니다. (ex. IoC, DI, Bean, Container ...)
- 기본적인 스프링의 어노테이션을 파악합니다. (ex. RestController, @RequestBody, @RequestParam...)
- 직렬화와 역직렬화를 이해합니다.
- 어떤 것을 Bean으로 등록할지 고민 합니다.
- 패키지를 잘 나눠주세요.
- checked exception, unchecked exception의 차이를 공부합니다.
- CustomException 적용과 예외 처리를 신경써주세요.

### 미션 내용

- Java 미션에서 진행한 레이싱 경주를 API 서버로 만듭니다.
- 먼저 복습 겸 console 프로그램을 만든 후 도메인 테스트를 모두 진행한 후 API 서버로 변경을 진행합니다.
- `콘솔 프로그램 + API 서버` 모두 이용할 수 있어야합니다.
- 콘솔과 API 서버 사이의 최대한 중복 코드가 생기지 않게 구조를 설계 해주세요.

### API 문서 (응답 값은 따로 정해진 것이 없다면 자유)

#### 1. 자동차 이름 등록 (POST)

Request

```
POST /api/cars

{
    "name" : "jay,pobi,crong",
    "tryCount" : 10
}

```

#### 2. 자동차 경주 시작 (POST)

Request

```
POST /api/cars/racing
```

#### 3. 자동차 경주 결과 조회 (GET)

Request

```
GET /api/cars
```

Response

```json
{
  "winner": "pobi",
  "status": [
    {
      "jay": 3
    },
    {
      "pobi": 5
    },
    {
      "crong": 1
    }
  ]
}
```

#### 4. 자동차 경주 결과 개별 조회 (GET)

Request

```
GET /api/cars?name=자동차명
```

Response

GET /api/cars?name=pobi

```json
{
  "pobi": 5
}
```

---

## 3-2. mission-lotto

### 미션 설명

- 조금 더 복잡한 스프링 API 서버를 만드는 연습을 합니다.
- console 프로그램은 생략하고 API 서버만 만듭니다.
- RESTful과 HTTP 메서드에 대해서 학습합니다.
- JPA에 대해서 학습합니다.
- API 문서는 본인 스스로 제작하고, 제출 시점에 문서로 이유와 함께 정리해서 같이 제출합니다.
- 데이터베이스(h2)를 활용해서 로또 결과를 저장하고 조회합니다.
    - JPA를 사용하는 이유를 생각해보기
    - JPA의 원리 파악하기
    - JPA의 특징 파악하기

### 미션 내용

- 다음과 같은 기능을 구현합니다.
    - 사용자 등록시 `이름과 소유 금액`을 함께 저장합니다.
    - 사용자는 로또를 n장 구매할 수 있습니다. 로또의 가격은 1000원입니다.
    - 로또를 구매한 후 남은 금액이 있다면 추가적으로 구매할 수 있습니다.
    - 로또는 구매 시점에 랜덤 번호로 발급이 됩니다. (수동 구매 없습니다.)
    - 특정 사용자가 지금까지 뽑은 `모든 로또의 번호와 당첨 여부`를 함께 확인할 수 있습니다.
    - 특정 사용자가 지금까지 뽑은 `특정 로또의 번호와 당첨 여부`를 확인할 수 있습니다.
    - `모든 사용자의 구매 로또 개수와 당첨 금액`을 확인할 수 있습니다.

---

## 3-3. mission-board

### 미션 설명

- 간단 게시판 구현하기
    - 회원가입 및 로그인 구현
    - 게시판 CRUD
    - 마이페이지 구현

- 쿠키, 세션, JWT 로그인 방식의 차이와 원리를 이해합니다.
- HandlerMethodArgumentResolver로 로그인 중복 로직을 제거 합니다.
- DispatcherServlet과 스프링 생명주기에 대해 공부합니다.
- Filter, Interceptor의 원리와 스프링 구조 전체 흐름에 맞게 공부합니다.
- 연관관계에 대해 알아봅니다.
- 스웨거 / REST Docs 중 선택하여 문서화를 진행합니다.
- EC2에 배포합니다.
