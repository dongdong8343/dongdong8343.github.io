---
title: "HTTP 개념 정리(6) - HTTP 상태코드"
excerpt: "HTTP 상태코드"

categories:
  - Etc
tags:
  - [HTTP 상태코드]
sidebar:
  nav: "counts"
---

### 상태코드

- 클라이언트가 보낸 요청의 처리 상태를 알려줌.
- 미래에 새로운 코드가 나오더라도 큰 범위에서 해석하면 됨.
  ex) 만약에 451이라는 코드가 없었는데 새로 나오더라도 4xx로 처리하면 됨 → 클라이언트 오류

### 상태코드 종류

- ~~1xx (Informational): 요청이 수신되어 처리중~~ → 잘 사용 안함.
- **2xx (Successful): 요청 정상 처리**
  - 범위가 많아서 다 쓰기 어렵다. → 팀 내부에서 범위를 한정해서 쓰는게 좋음
  - 200 Ok
      <div align="center">
       <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/69251892-befb-4e47-90a5-ca137f974827" width="80%" height="auto" />
      </div>

  - 201 Created → 클라이언트가 POST 요청 시 서버에 리소스가 잘 생성되면 201 메시지 보냄
      <div align="center">
          <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/cda5a0e2-805f-4fb9-b763-2b59f04cc439" width="80%" height="auto" />
      </div>

  - 202 Accepted → 요청은 접수됨, 처리가 완료되지 않음. (잘 안씀)
  - 204 No Content → 요청이 성공적으로 처리는 됐지만 응답 메시지 본문에 보낼 데이터 없는 경우
    ex) 웹 문서 편집기 save 버튼 → 저장하고 바뀌는거 없음. (204 메시지로 잘 처리됐는지 확인)
- **3xx (Redirection): 요청을 완료하려면 추가 행동이 필요**
  - 리다이렉트
    브라우저가 3xx 응답의 결과에 Location 헤더가 있으면 Location 위치로 이동시킴
  - 리다이렉션 종류
    - 영구 리다이렉션 - 특정 리소스의 URI가 영구적으로 이동

      - 301 - 리다이렉트 요청하면 GET으로 변하고 본문 제거될 수 있음.
          <div align="center">
           <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/ece90257-cc9b-42a3-a4de-43c4030753a7" width="80%" height="auto" />
          </div>

      - 308 - 리다이렉트 요청 메서드와 본문 유지
          <div align="center">
           <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/dd25168b-8fc8-4bab-b4b6-3f43cdb91946" width="80%" height="auto" />
          </div>


    - 일시 리다이렉션 - 리소스 URI가 일시적으로 변경(실무에서 많이 씀)

      - ex) 배달 완료 후 배달 주문 내역으로 이동 (PRG - POST/REDIRECT/GET)
        POST로 주문 후 새로고침 시 다시 요청되므로 중복 주문이 될 가능성을 막아야 함.
        - PRG 사용 전 - POST 요청 후 새로고침하면 POST 요청이 돼서 중복 주문이 들어감.
          <div align="center">
           <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/e82e5ae7-c53c-4664-96fd-a0f3b9b1c0fc" width="80%" height="auto" />
          </div>
          
          - PRG 사용 후 - POST 요청 후 GET 메서드로 REDIRECT 후 새로고침을 해도 GET 요청이 되면서 중복 주문 막음.
          
          <div align="center">
           <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/77db5a30-071e-470e-890a-4e51a7814e17" width="80%" height="auto" />
          </div>

      - 302 Found - 리다이렉트시 요청 메소드가 GET으로 변하고, 본문 제거 될 수 있다.(명확하지 않다.)
      - 303 See Other - 리다이렉트시 무조건 요청 메소드 GET으로 변경
      - 307 Temporary Redirect - 리다이렉트시 요청 메소드, 본문 변경 x
      - 303, 307 권장하지만 이미 많은 곳에서 302를 기본 값으로 사용함.

    - 특수 리다이렉션 - 결과 대신 캐시를 사용하도록 함.
      - 304 Not Modified
        리소스가 수정되지 않았음을 알려줌.(로컬 PC에 저장된 캐시를 쓰라는 뜻) → 캐시로 리다이렉트 함.
        요청 메시지 포함 안한다. (캐시를 사용하면 되기 때문에)
- **4xx (Client Error): 클라이언트 오류**
  - 클라이언트가 잘못한 경우(문법 오류 등) → 똑같은 요청 보내면 똑같이 오류가 남.
  - 400 Bad Request - 요청, 메시지 오류 → 다시 검토하고 보내야 함.
    ex) 요청 파라미터, API 스펙 잘못된 경우
  - 401 Unauthorized - 리소스에 대한 인증이 안된 경우
    오류 발생 시 응답에 WWW-Authenticate 헤더와 함께 인증 방법 설명
  - 403 Forbidden - 인증은 했지만 리소스 접근 권한이 없는 경우
    ex) 어드민 등급이 아닌 사용자가 로그인은 했지만 어드민 등급 리소스에 접근하는 경우
  - 404 Not Found - 요청 리소스를 찾을 수 없는 경우
    사용자가 권한이 부족한 리소스에 접근할 때 숨기고 싶을 때
- **5xx (Server Error): 서버 오류**
  - 최대한 5xx 에러 만들면 안됨.
  - 서버 문제 → 요청 재시도하면 성공할 수도 있음(복구가 되면)
    - DB 내려감.
    - 쿼리에 문제
    - NullPointerException 등
  - 500 Internal Server Error - 서버 내부 문제(애매하면 500 오류)
  - 503 Service Unavailable - 서버 일시적으로 과부화 or 작업으로 잠시 요청 처리 불가
    Retry-After 헤더 필드로 언제 복구되는지 보낼 수 있음.

---

- 김영한님의 모든 개발자를 위한 HTTP 웹 기본 지식을 수강하면서 정리한 내용입니다.
