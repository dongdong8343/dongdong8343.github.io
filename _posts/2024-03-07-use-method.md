---
title: "HTTP 개념 정리(5) - HTTP 메서드 활용"
excerpt: "HTTP 메서드 활용"

categories:
  - Etc
tags:
  - [HTTP 메서드]
sidebar:
  nav: "counts"
---

# 섹션 5 - HTTP 메서드 활용

## 클라이언트에서 서버로 데이터 전송

1. **쿼리 파라미터를 통해 데이터 전송**
   - GET에 주로 사용
   - 검색어 칠 때 주로 사용
2. **메시지 바디를 통해 데이터 전송**
   - POST, PUT, PATCH에 주로 사용
   - 회원 가입, 상품 주문, 리소스 등록, 리소스 변경

### 4가지 상황

1. **정적 데이터 조회(이미지, 정적 텍스트 문서)**

   - GET 사용
   - 쿼리 파라미터 미사용 → 리소스 경로만으로 조회 가능
       <div align="center">
        <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/7214adb0-994e-42cb-af3b-a95dceb30f54" width="80%" height="auto" />
       </div>


1. **동적 데이터 조회**

   - 검색, 게시판 목록 정렬, 필터에서 주로 사용
   - GET 사용 → 쿼리 파라미터 사용
       <div align="center">
         <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/e3a850ae-3f73-4ba7-9d4c-7fe4d0997cc4" width="80%" height="auto" />
       </div>


1. **HTML FORM 데이터 전송 → GET, POST만 지원**

   - POST 전송 - FORM에 입력한 데이터를 가지고 요청 메시지를 만들어서 서버로 전송

     Content-Type: application/x-www-form-urlencoded 사용

     form의 내용들을 key = value 형식으로 메시지 바디를 통해서 전송

     전송 데이터를 url encoding 처리

     ex) abc김 → abc%EA%B9%80

       <div align="center">
           <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/b31aa52f-3a35-40ec-af21-c14edc659efa" width="80%" height="auto" />
       </div>


   - GET 전송 - 조회

       <div align="center">
        <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/0c0672e6-ba07-41b8-8f08-3b5b3168c229" width="80%" height="auto" />
       </div>


   - multipart/form-data
     Content-Type: multipart/form-data
     파일 업로드 같은 바이너리 데이터 전송할 때 주로 사용
     다른 종류의 여러 데이터 전송할 때 사용
       <div align="center">
        <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/154d21f5-ec6d-4b33-a36a-f13c4dfefbe6" width="80%" height="auto" />
       </div>


1. **HTTP API 데이터 전송**

   - HTML FORM을 사용하지 않는 경우
   - 서버끼리 통신할 때 사용
   - 앱 클라이언트(아이폰, 안드로이드)
   - 웹 클라이언트(자바스크립트 통해서 통신)
   - Content-Type: application/json을 주로 사용

   <div align="center">
       <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/fa6b3d33-65ac-4124-94ad-e1b4dc81769a" width="80%" height="auto" />
   </div>

## HTTP API 설계 예시

### 회원 관리 시스템 API 설계 - POST 기반 등록

- 회원 목록 /members → GET
- 회원 등록 /members → POST
- 회원 조회 /members/{id} → GET
- 회원 수정 /members/{id} → PATCH(부분 수정에 좋음), PUT(회원 데이터 한, 두 개 빠지면 큰 일, 게시판 수정할 때는 좋음), POST
- 회원 삭제 /members/{id} → DELETE

  **POST 기반 등록 특징**

- 클라이언트는 등록될 리소스의 URI를 모른다. → 서버가 새로운 리소스 URI를 생성해줌.
- **위와 같은 형식을 컬렉션(Collection)이라고 함. → 주로 사용**
  - 서버가 관리하는 리소스 디렉토리
  - 서버가 URI 생성, 관리
  - 여기서 컬렉션은 /members

### 파일 관리 시스템 API 설계 - PUT 기반 등록

- 파일 목록 /files → GET
- 파일 조회 /files/{filename} → GET
- 파일 등록 /files/{filename} → PUT (클라이언트가 filename을 알기 때문에 PUT을 씀)
- 파일 삭제 /files/{filename} → DELETE
- 파일 대량 등록 /files → POST

  **PUT 기반 등록 특징**

- 클라이언트가 리소스 URI를 알고 있어야 함. → 클라이언트가 직접 리소스의 URI 지정
- **위와 같은 형식을 스토어(Store)라고 함.**
  - 클라이언트가 관리하는 리소스 저장소
  - 클라이언트가 리소스의 URI 알고 관리
  - 여기서 스토어는 /files

### HTML FORM 사용 → GET, POST만 사용 가능

- 회원 목록 /members -> GET
- 회원 등록 폼 /members/new -> GET
- 회원 등록 /members/new, /members -> POST
- 회원 조회 /members/{id} -> GET
- 회원 수정 폼 /members/{id}/edit -> GET
- 회원 수정 /members/{id}/edit, /members/{id} -> POST
- 회원 삭제 /members/{id}/delete -> POST

위 경우 GET, POST만 있어서 삭제, 수정 같은걸 하는 경우 처리해줄 메서드가 없음.

⇒ 컨트롤 URI 사용해야 함. (동사로 된 리소스 경로 사용)

**※ 최대한 리소스 중심으로 URI를 설계하고 정 안되는 경우들은 컨트롤 URI를 사용**

ex) /new, /edit, /delete가 컨트롤 URI

---

- 김영한님의 모든 개발자를 위한 HTTP 웹 기본 지식을 수강하면서 정리한 내용입니다.
