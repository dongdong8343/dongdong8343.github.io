---
title: "게시판 만들기 2 - 뷰 템플릿과 MVC"
excerpt: "뷰 템플릿과 MVC"

categories:
  - Spring
tags:
  - [localhost, port]
sidebar:
  nav: "counts"
---

### 뷰 템플릿과 MVC

- **뷰 템플릿**
  웹 페이지를 하나의 툴로 만들고 데이터에 따라 다르게 표시할 부분에 변수를 삽입해서 서로 다른 페이지로 보여줍니다.
  스프링 부트 프로젝트를 만들 때 머스테치(Mustache)라는 도구를 추가했는데 이 도구가 뷰 템플릿을 만드는 도구입니다.
- **MVC**
  M(Model) - 데이터를 관리하는 역할을 합니다.
  V(View) - 위에서 설명한 뷰 템플릿을 의미합니다.
  C(Controller) - 클라이언트의 요청을 처리하는 역할을 합니다.

### MVC의 역할과 실행 흐름

- 컨트롤러 - 클라이언트의 요청 받음
- 뷰 - 최종 페이지 만듦
- 모델 - 뷰에 데이터를 전달

### hi 페이지의 실행 흐름

<파일 구조>

<div align="center">
   <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/590ada20-17a6-43d4-8b3a-37b296223e90" width="50%" height="auto" />
   </div>
1. **클라이언트가 url에 요청 입력**
    
   <div align="center">
   <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/1ed4a137-c829-442d-a9df-91ace71815e3" width="50%" height="auto" />
   </div>
    
2. **컨트롤러가 url의 요청에 따라 메서드를 수행**
3. **모델 객체를 매개 변수로 가져오고 변수를 생성해서 뷰 템플릿에 데이터 전달** 
    
    → 변수에 따라 다른 뷰 템플릿 페이지 출력
    
4. **메서드를 끝내기 전에 파일 이름을 반환**
    
    ```java
    package com.example.firstproject.controller;
    
    import org.springframework.stereotype.Controller;
    import org.springframework.ui.Model;
    import org.springframework.web.bind.annotation.GetMapping;
    
    @Controller // 컨트롤러임을 선언하는 어노테이션
    public class FirstController {
        @GetMapping("/hi") // url에 localhost:8080/hi로 접속하면 greetings.mustache 파일을 반환하라는 뜻
        public String niceToMeetYou(Model model){ // model을 통해 변수 등록 가능해짐.
            model.addAttribute("username", "동동");
            return "greetings"; // greetings.mustache 파일 반환
        }
        @GetMapping("/bye")
        public String byeMan(Model model){
            model.addAttribute("username", "동동");
            return "goodbye";
        }
    }
    ```
    
5. **templates 디렉터리에서 해당 파일을 찾아서 웹 브라우저로 전송함.**
    
    doc 입력하고 tab키 누르면 아래 구조 바로 입력됨.
    
    ```java
    // 파일 이름 : greetings.mustache
    <html>
    <head>
        <meta charset="UTF-8">
        <meta name="viewport"
              content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <title>Document</title>
    </head>
    <body>
        <h1>{{username}}님 ️안녕하세요!</h1>
    </body>
    </html>
    ```
