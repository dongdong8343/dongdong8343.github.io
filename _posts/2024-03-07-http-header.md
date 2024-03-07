---
title: "HTTP 개념 정리(7) - HTTP 헤더1 - 일반 헤더"
excerpt: "HTTP 헤더1 - 일반 헤더"

categories:
  - Etc
tags:
  - [HTTP 헤더1 - 일반 헤더]
sidebar:
  nav: "counts"
---

## HTTP 헤더

• header-field = field-name ":" OWS field-value OWS (OWS:띄어쓰기 허용)

<div align="center">
    <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/c6b60159-d48c-4708-91a7-e70dca896d43" width="80%" height="auto" />
</div>

- HTTP 전송에 필요한 모든 부가정보
  ex) 메시지 바디의 내용, 메시지 바디의 크기, 압축, 인증, 요청 클라이언트, 서버 정보, 캐시 관리 정보 등

## HTTP 헤더 - RFC2616(과거) : 폐기됨.

<div align="center">
    <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/4860b48e-978f-43d4-b481-b2b5bf22e1d3" width="80%" height="auto" />
</div>
- General 헤더: 메시지 전체에 적용되는 정보, 예) Connection: close
- Request 헤더: 요청 정보, 예) User-Agent: Mozilla/5.0 (Macintosh; ..)
- Response 헤더: 응답 정보, 예) Server: Apache
- Entity 헤더: 엔티티 바디 정보, 예) Content-Type: text/html, Content-Length: 3423

<div align="center">
    <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/b4d655f0-efcd-4f11-9910-6f60231e56d5" width="80%" height="auto" />
</div>

- 메시지 본문은 엔티티 본문 전달을 위함.
- 엔티티 본문 - 요청, 응답에서 전달할 실제 데이터
- 엔티티 헤더 - 엔티티 본문의 데이터 해석하기 위한 정보 제공(데이터 유형, 데이터 길이, 압축 정보 등등)

## HTTP 헤더 - RFC723x(현재)

- 엔티티가 표현으로 바뀜.
- 표현 = 표현 메타데이터 + 표현 데이터

<div align="center">
    <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/367f0da3-0184-4761-804f-46f7daaa9420" width="80%" height="auto" />
</div>

- 메시지 본문(=페이로드)을 통해 표현 데이터 전달
- 표현은 요청이나 응답에서 전달할 실제 데이터
- 표현 헤더 - 표현 데이터를 해석할 수 있는 정보 제공(데이터 유형, 데이터 길이, 압축 정보 등등)

## 표현

### Content-Type

- 표현 데이터 형식 설명 (”body에 들어가는 데이터 타입이 뭐냐?”)

<div align="center">
    <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/8cea4739-ce36-43cf-9e84-489f502de15d" width="80%" height="auto" />
</div>

### Content-Encoding

- 표현 데이터 압축하기위함.
- 데이터 전달하는 곳 : 압축 후 엔코딩 헤더 추가
- 데이터 읽는 쪽 : 엔코딩 정보로 압축 해제

<div align="center">
    <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/16d2a1c3-648e-47f0-88ed-ff1b713a8017" width="80%" height="auto" />
</div>

### Content-Language

- 표현 데이터의 자연 언어를 표현
- 한국 사람인데 영어로 오면 클라이언트에서 한글로 수정 가능하게 바꿀 수도 있음.

<div align="center">
    <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/eae11b8e-40fe-4542-8120-5928db352a98" width="80%" height="auto" />
</div>

### Content-Length

- 표현 데이터의 길이(바이트 단위)
- Transfer-Encoding(전송 코딩)을 사용하면 Content-Length를 사용하면 안됨

<div align="center">
    <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/259b01bd-fde0-43ab-8d0e-2daf611b2d7e" width="80%" height="auto" />
</div>

## 협상(콘텐츠 네고시에이션)

- 클라이언트가 원하는 표현 요청

<div align="center">
    <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/f4d568d9-78cb-4449-8a62-f7393d3fb649" width="80%" height="auto" />
</div>

### Accept

- 클라이언트가 선호하는 미디어 타입 전달

### Accept-Charset

- 클라이언트가 선호하는 문자 인코딩

### Accept-Encoding

- 클라이언트가 선호하는 압축 인코딩

### Accept-Language

- 클라이언트가 선호하는 자연 언어

**Accept-Language 적용 전**

다중 언어 지원하지만 선호하는 언어 요청 안하면 우선 순위가 높은 언어를 응답해줌.

<div align="center">
    <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/a3853a62-c899-4e07-9146-573cccc8fedb" width="80%" height="auto" />
</div>

**Accept-Language 적용 후**

요청한 언어가 지원되면 맞게 전달해줌.

<div align="center">
    <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/1797dc90-fe6d-43f6-907e-b5d2eb7f0037" width="80%" height="auto" />
</div>

**Accept-Language 적용했지만 지원 안되는 언어를 요청한 경우**

<div align="center">
    <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/4730fbdf-84cd-4b1e-86a4-03bfb4c1afc4" width="80%" height="auto" />
</div>

### 협상과 우선순위

```
GET /event
Accept-Language: ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7
```

- 0~1, 높을수록 우선순위 높다. ⇒ 생략하면 1

<div align="center">
    <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/3cbb2242-28d4-4a26-ac41-9b1135f0a11a" width="80%" height="auto" />
</div>

```
GET /event
Accept: text/*, text/plain, text/plain;format=flowed, */*
```

- 구체적인게 우선순위 높다.

1. text/plain;format=flowed
2. text/plain
3. text/\*
4. **/**

```
Accept: text/*;q=0.3, text/html;q=0.7, text/html;level=1,
text/html;level=2;q=0.4, */*;q=0.5
```

- 구체적인 것을 기준으로 미디어 타입 맞춘다.

| Media Type        | Quality |
| ----------------- | ------- |
| text/html;level=1 | 1       |
| text/html         | 0.7     |
| text/plain        | 0.3     |
| image/jpeg        | 0.5     |
| text/html;level=2 | 0.4     |
| text/html;level=3 | 0.7     |

## 전송 방식

### 단순 전송

- Content-Length 알 때 → 한 번에 다 요청하고 쭉 받음.

<div align="center">
    <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/07c70e34-e1e3-46ac-b0ff-12b5a29f999b" width="80%" height="auto" />
</div>

### 압축 전송

- 압축해서 전송하는 방식
- Content-Encoding 넣어야 함. → 이 정보를 보고 클라이언트에서 압축을 풀기 때문이다.

<div align="center">
    <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/d734a0c9-e43a-4a03-bedd-2053c66286b0" width="80%" height="auto" />
</div>

### 분할 전송

- 분할해서 전송하는 방식
- 용량이 큰 경우 한번에 쫙 보내면 오래 걸림. → 용량이 큰 경우 분할해서 받을 수 있음(분할 전송)
- 끝나면 0으로 표시하고 /r/n 전달해줌.
- Content-Length를 쓰면 안됨
  → Content-Length를 예상하지도 못하고 chunked안에 바이트 정보를 포함한다.

<div align="center">
    <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/3e3d756f-af80-4c3a-ac8a-6b37c2fe2cd4" width="80%" height="auto" />
</div>

### 범위 전송

- 전달을 받다가 중간에 끊기면 클라이언트에서 중간부터 전달해달라고 요청할 수 있음.

<div align="center">
    <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/251a2f5e-dad5-4db6-a591-19d646684854" width="80%" height="auto" />
</div>

## 일반 정보

### From

- 클라이언트의 이메일 정보
- 검색 엔진 같은 곳에서 주로 사용
- 요청에서 사용

### Referer

- 이전 웹 페이지의 주소
- a → b 이동 시 b를 요청할 때 Referer : a를 포함해서 요청
- 유입 경로 분석 o (데이터 분석)
- 요청에서 사용

### User-Agent

```
user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/
537.36 (KHTML, like Gecko) Chrome/86.0.4240.183 Safari/537.36
```

- 클라이언트의 애플리케이션 정보
- 특정 브라우저에서만 버그 생기는 경우 파악 가능
- 유저들이 어떤 브라우저에서 많이 들어오는지 파악 가능
- 요청에서 사용

### Server

```
Server: Apache/2.2.22 (Debian)
Server: nginx
```

- 요청을 처리하는 ORIGIN 서버(프락시 서버가 아닌 응답을 하는 서버를 의미)의 소프트웨어 정보
- 응답에서 사용

### Date

```
Date: Tue, 15 Nov 1994 08:12:31 GMT
```

- 메시지가 발생한 날짜와 시간
- 응답에서 사용

## 특별한 정보

### Host

<div align="center">
    <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/1bee8677-5e69-48b1-9885-12c61a84168c" width="80%" height="auto" />
</div>

- 요청한 호스트 정보
- 하나의 서버가 여러 도메인을 가지는 경우도 있음. 이런 서버에 요청할 때 어느 도메인으로 가라고 명시안하면 서버 입장에서는 어디로 요청을 보내야할지 모른다. ⇒ Host는 필수로 작성해야한다.
    <div align="center">
     <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/91badfb4-a9c7-4d98-8a56-41b54f9ff918" width="80%" height="auto" />
    </div>


### Location

- 201 (Created) ⇒ Location 값은 생성된 리소스의 URI를 의미한다.
- 3xx (Redirected) ⇒ Location 값은 자동으로 리다이렉션 위한 대상 리소스를 가리킨다.

### Allow

- 허용 가능한 HTTP 메서드를 알려줌.
- 405 (Method Not Allowed) 응답에 포함됨.
- ex) Allow: GET, HEAD, PUT
  - POST 메서드가 없는데 POST로 요청을 보내면 서버에서 POST 메서드는 없고 GET, HEAD, PUT 메서드만 존재한다고 알려줌.

### Retry-After

- 클라이언트가 다음 요청까지 기다려야 하는 시간
- 503 (Service Unavailable): 서비스가 언제까지 불능인지 알려줄 수 있다.

> Retry-After: 120 (초단위 표기)
>
> Retry-After: Fri, 31 Dec 1999 23:59:59 GMT (날짜 표기)

## 인증

### Authorization

- 클라이언트 인증 정보를 서버에 전달
- Authorization: 인증과 관련된 값

### WWW-Authenticate

- 리소스 접근시 필요한 인증 정보 정의
- 401 Unauthorized 응답에 포함되는 헤더
- WWW-Authenticate: Newauth realm="apps", type=1,
  title="Login to \"apps\"", Basic realm="simple"
- 클라이언트가 인증을 잘못하면 제대로 된 인증 정보를 만들라고 위와 같은 식으로 인증 정보를 주고 이걸 참고하라고 한다.

## 쿠키

**Set-Cookie ⇒ 서버에서 클라이언트로 쿠키 전달**

**Cookie ⇒ 클라이언트가 전달 받은 쿠키 저장함. 클라이언트가 서버로 요청할 때 쿠키 전달**

### 쿠키 미사용해서 로그인 하는 경우

1. 처음 welcome 페이지 접속

<div align="center">
 <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/4dc0dab3-af37-4805-838a-1b38cf14ba9a" width="80%" height="auto" />
</div>

2. user 정보를 넣어서 로그인을 함.

<div align="center">
 <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/e1ddea4e-0b4a-4045-b887-b3cd0caf11fb" width="80%" height="auto" />
</div>

3. 로그인 후 다시 welcome 페이지 접속

<div align="center">
    <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/b2d5aaf3-bad9-41b5-8c8f-71cc827f6d72" width="80%" height="auto" />
</div>

위처럼 한 번 로그인 했다가 다시 접속하면 user를 기억하지 못하고 손님으로 응답해주는 것을 볼 수 있다.

**왜 이럴까?**

Stateless 속성 때문이다. 기본적으로 HTTP는 요청과 응답이 끝나면 응답을 끊는다.(무상태 프로토콜)

클라이언트가 다시 요청하면 이전 정보를 기억하지 못한다.

**어떻게 해결할 것인가?**

<div align="center">
    <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/03d2dc8d-3f39-43e2-a08c-85daacda272c" width="80%" height="auto" />
</div>

요청할 때마다 user 정보를 포함해서 보낼 수 있다. 하지만 요청할 때마다 계속 포함해서 보낼 수는 없는 노릇이다. → 모든 요청에 사용자 정보가 포함되도록 개발해야 한다. (매우 힘들다.)

**그럼 어떻게 해결할 것인가?**

그래서 쿠키가 있다.

사용자가 로그인을 하면 서버에서 쿠키를 만들어서 클라이언트로 전송해준다. 그럼 클라이언트 측에서 쿠키 저장소에 쿠키를 저장한다.

<div align="center">
    <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/0f8e2cc2-7508-4e17-9175-e5f6c7098fc9" width="80%" height="auto" />
</div>

그럼 로그인 이후 HTTP 요청할 때마다 쿠키 저장소를 뒤져서 쿠키를 전송한다.

모든 요청에 쿠키 정보가 포함됨.

<div align="center">
    <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/6954c374-d9d5-4833-bbfc-a4848bf66c63" width="80%" height="auto" />
</div>

### 쿠키에 대한 설명

```
set-cookie: sessionId=abcde1234; expires=Sat, 26-Dec-2020 00:00:00 GMT; path=/; [domain=.google.com](http://domain=.google.com/); Secure
```

- 사용처
  - 사용자 로그인 세션 관리
  - 광고 정보 트래킹
- 요청마다 쿠키 정보는 서버에 전송된다.
  - 네트워크 트래픽이 추가로 유발된다.
  - 최소한의 정보만 사용(세션 id, 인증 토큰)
  - 필요할 때마다 꺼내서 사용할 수 있는 웹 스토리지라는 개념도 있다.
- 보안에 민감한 데이터는 저장하면 큰일난다.

### 쿠키 - 생명주기 (Expires, max-age)

- Set-Cookie: expires=Sat, 26-Dec-2020 04:39:21 GMT
  - 저 만료일이 되면 쿠키가 삭제된다.
- Set-Cookie: max-age=3600 (3600초)
  - 3600초 뒤에 쿠키가 삭제된다.
- 세션 쿠키 → 만료 날짜를 생략하면 브라우저 종료까지만 유지
- 영속 쿠키 → 만료 날짜를 입력하면 해당 날짜까지 유지

### 쿠키 - 도메인 (Domain)

- 명시한 경우
  - 명시한 문서, 서브 도메인에서 쿠키 접근 가능
  - domain=example.org를 지정해서 쿠키를 생성한다.
  - example.org, dev.example.org에서도 사용 가능
- 생략한 경우
  - example.org에서 쿠키 생성하고 domain 지정을 생략하면 example.org에서만 쿠키 접근 가능하고 다른 도메인에서는 접근 불가능

### 쿠키 - 경로 (Path)

- path=/home
- 위처럼 지정하면 /home을 포함한 하위 경로에서만 쿠키 접근 가능
  - /home (가능)
  - /home/level1 (가능)
  - /home/level1/level2 (가능)
  - /hello (불가능)
- 일반적으로 path=/ 루트로 지정

### 쿠키 - 보안 (Secure, HttpOnly, SameSite)

- Secure
  - 쿠키는 http, https 구분 없이 전송
  - Secure를 적용하면 https에서만 전송
- HttpOnly
  - XSS 공격 방지
    XSS 공격이란?
    공격자가 악의적인 스크립트를 삽입해서 사용자의 세션 쿠키를 탈취하려는 공격
  - 자바스크립트에서 쿠키 접근 불가
  - HTTP 전송에만 사용
- SameSite
  - XSRF 공격 방지
    XSRF 공격이란?
    사용자가 의도한 행동이 아닌 공격자가 의도한 행동을 웹 애플리케이션에서 실행하게 만드는 공격 기법
  - 요청 도메인과 쿠키에 설정된 도메인이 같은 경우만 쿠키 전송

---

- 김영한님의 모든 개발자를 위한 HTTP 웹 기본 지식을 수강하면서 정리한 내용입니다.
