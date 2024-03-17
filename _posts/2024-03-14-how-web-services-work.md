---
title: "게시판 만들기 1 - 웹 서비스 동작 원리"
excerpt: "웹 서비스 동작 원리"

categories:
  - Spring
tags:
  - [localhost, port]
sidebar:
  nav: "counts"
---

### 웹 서비스 동작 원리

원리를 설명하기 전에 일단 웹에서 보여질 페이지를 하나 생성해서 실행을 해보겠습니다.

1. src > main > resources > static 폴더에서 우클릭해서 hello.html파일을 하나 만들어 주겠습니다.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Title</title>
  </head>
  <body>
    <h1>동동</h1>
  </body>
</html>
```

1. 웹을 실행해서 http://localhost:8080/hello.html 주소를 입력하고 엔터를 칩니다.

   그럼 다음과 같은 화면이 나옵니다.

   <div align="center">
   <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/67f29cec-5b12-47fc-8a77-e7e381b1be6f" width="80%" height="auto" />
   </div>

지금부터 어떻게 저렇게 실행이 되는지 차근차근 설명해보겠습니다.
**클라이언트 - 서버 구조로 이루어져 있습니다.**

클라이언트가 요청을 하면 서버에서 응답을 해주는 방식을 의미합니다.

위에서 실습한 내용도 클라이언트가 요청을 해서 서버에서 응답을 한 결과를 화면에서 본 것입니다.

그래서 동작이 원활하게 이루어지려면 당연히 서버가 동작하고 있어야합니다.

아래와 같이 메인 메서드를 실행하겠습니다.

<div align="center">
    <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/5022a149-dab7-41ac-85e5-b8a35bf6a247" width="80%" height="auto" />
</div>

실행을 하면 아래와 같이 서버가 잘 실행이 된다고 콘솔창에서 확인 가능합니다.

<div align="center">
    <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/80ef1849-f4fc-4ee7-b5f2-50954bc3cef4" width="80%" height="auto" />
</div>

톰캣이 8080 포트에서 실행이 됐다는 의미입니다.

톰캣은 간단하게 설명하자면 웹 서버를 의미합니다. 추후에 따로 정리해서 포스팅하겠습니다.

서버가 실행이 되면 아래와 같이 에러 페이지이지만 접근할 수 있는 것을 볼 수 있습니다.

<div align="center">
    <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/00734e14-7dad-4524-a6e8-9160a40ee33f" width="80%" height="auto" />
</div>

http://localhost:8080/hello.html 이 주소로 접속했을 때 어떻게 화면이 보이게 되는건지 설명하겠습니다.

- localhost
  내가 사는 집을 ‘우리 집’이라고 표현하는 것과 같습니다.
  즉 내 컴퓨터의 주소를 뜻합니다.
- 8080
  포트 번호를 의미합니다.
  저 포트 번호에서 스프링 부트가 동작하고 있고 저 방으로 클라이언트가 요청을 보내는 것입니다.
  포트에 대한 자세한 정리는 아래 링크를 참고하면 됩니다.

  [포트 설명](https://dongdong8343.github.io/etc/internet-network/)

- hello.html
  이건 그냥 파일 이름입니다. 아까 위에서 만들었던 html 파일입니다.

즉 정리를 해보자면 내 컴퓨터의 8080 포트에서 실행되고 있는 스프링 부트에 hello.html 파일을 요청한겁니다. 요청을 하면 스프링 부트는 기본적으로 src > main > resources > static 디렉터리에서 파일을 찾습니다. 그리고 파일을 찾았다면 클라이언트에 응답해줍니다.

그래서 제가 작성한 html 파일을 만나볼 수 있었습니다.
