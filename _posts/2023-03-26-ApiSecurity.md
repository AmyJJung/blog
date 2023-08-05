---
layout: post
title: JWT 토큰
tags:
  - API 
---

<br>

> 회사에서 API 보안관련 회의를 하다가 JWT (JSON Web Token)에 대한 이야기가 나왔다. JWT를 사용할 경우 기존 세션 인증 방식과는 다른 장점이 존재한다. 하지만 결국 이 토큰도 악의적인 해커에 의해 탈취당하면 무용지물이다. 그럼 조금이라도 토큰을 안전하게 사용하려면 클라이언트는 JWT를 어디에 보관해야 하는걸까? 이번 글에서는 JWT의 기본 개념과 세션 인증 방식과의 차이점, 그리고 클라이언트 저장소에 대한 내용들을 정리해 볼 예정이다. 
>
> 내가 이번 글을 정리하면서 찾아본 개념들은 다음과 같다 
>
> ` JWT`, `Cookie`,  `Session`,  `HttpOnly`,  `Secure`,  `XSS`,  `CSRF`, `CSRF Token`, `Refresh Token`,  `Authentication`,  `Authorization` , `SOP`, `CORS`, `Same Site`

<br>









---

- 참고
  - [JWT 저장소에 대한 고민](https://cjw-awdsd.tistory.com/48)
  - [JWT 인증은 무엇이고 어떻게 사용해야 할까?](https://www.popit.kr/jwt-%EC%9D%B8%EC%A6%9D%EC%9D%80-%EB%AC%B4%EC%97%87%EC%9D%B4%EA%B3%A0-%EC%96%B4%EB%96%BB%EA%B2%8C-%EC%82%AC%EC%9A%A9%ED%95%B4%EC%95%BC-%ED%95%A0%EA%B9%8C/)
  - [HttpOnly와 Secure Cookie](https://theheydaze.tistory.com/550)
