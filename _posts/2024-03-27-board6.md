---
title: "게시판 만들기 6 - 게시글 수정 : Update"
excerpt: "게시글 수정"

categories:
  - Spring
tags:
  - [Update, 게시글 수정]
sidebar:
  nav: "counts"
---

- **데이터 수정 단계**

1.  **수정 페이지 만들고 기존 데이터 불러오기**

    a. 상세 페이지에서 Edit 버튼 클릭

       <div align="center">
     <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/2625ad7c-117d-4a41-a6d9-a8291de5c06e" width="100%" height="auto" />
     </div>

    b. 컨트롤러는 해당 글의 id로 DB에서 데이터 찾아서 가져옴

    c. 컨트롤러는 가져온 데이터를 뷰에서 사용할 수 있도록 모델에 등록

    ```java
       // 컨트롤러에 edit 메서드 생성
       @GetMapping("/articles/{id}/edit")
       // @PathVariable -> id를 매개변수로 받아옴
       public String edit(@PathVariable Long id, Model model){
       		// url에 입력된 id로 DB에 저장된 엔티티를 가지고 옴.
           Article articleEntity = articleRepository.findById(id).orElse(null);
           // 수정 페이지에 기존 데이터를 보여주기위해 엔티티를 모델에 등록
           model.addAttribute("article", articleEntity);
           return "articles/edit";
       }
    ```

    d. 모델에 등록된 데이터를 수정 페이지에 보여줌.

    <div align="center">
     <img src="https://github.com/dongdong8343/dongdong8343.github.io/assets/93115530/df1de4ab-008c-4c35-98e4-74d0d1bb343b" width="100%" height="auto" />
     </div>

2.  **데이터를 수정하고 DB에 반영하고 결과를 볼 수 있게 상세 페이지로 리다이렉트하기**

    a. 폼 데이터를 DTO에 담아 컨트롤러에서 받음.

    b. DTO를 엔티티로 변환

    c. DB에서 기존 데이터를 수정 데이터로 갱신

    d. 수정 데이터를 상세 페이지로 리다이렉트

    ```java
        @PostMapping("/articles/update")
        // form이 전송한 데이터는 DTO로 받는다. DTO는 메서드의 매개변수로 받아온다.
        public String update(ArticleForm form){
        	log.info(form.toString());
        	// DTO를 엔티티로 변환
        	Article updateArticle = form.toEntity();
        	// 엔티티를 DB에 저장
        	Article target = articleRepository.findById(updateArticle.getId()).orElse(null);
        	if(target != null){
        		articleRepository.save(updateArticle);
        	}
        	// 수정 결과 페이지로 리다이렉트하기
        	return "redirect:/articles/" + target.getId();
        }
    ```
