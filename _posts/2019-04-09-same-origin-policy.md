---
layout: post
title: same origin policy란?
permalink: posts/same-origin-policy
tag: javascript HTTP security
---

> 해당 포스트는 [https://en.wikipedia.org/wiki/Same-origin_policy](https://en.wikipedia.org/wiki/Same-origin_policy)를 번역하여 작성하였습니다. 잘못된 부분이 있다면 댓글 부탁드립니다.

컴퓨팅에서 same-origin policy는 웹 어플리케이션 보안에 있어서 중요합니다. 정책 안에서 same origin을 포함했다고 가정했을 때 브라우저는 두 번째 페이지에 있는 데이터에 접근하도록 첫 번째 페이지에 있는 스크립트가 동작할 수 있도록 허용합니다. 정책은 URI scheme, host name, port number을 포함해서 정의합니다. 이 정책은 페이지의 DOM을 통해 악의적으로 다른 페이지 민감한 정보에 접근할 수있는 스크립트가 실행되는 것을 방지합니다.

이 메카니즘은 인증된 유저세션을 유지하기위해 HTTP 쿠키에 의존하는 웹 어플리케이션에 중요한 의미가 있습니다. 서버는 HTTP 쿠키 정보를 통해 민감한 정보를 보여주거나 특정 액션을 취합니다. 관련없는 사이트와 컨텐츠를 엄격하게 분리하는 것은 클라이언트 사이드에서 데이터 손실을 막기위해 반드시 유지돼야 합니다.

same-origin policy는 스크립트에만 적용된다는 것을 인지하는 것은 굉장히 중요합니다. 이 말인즉슨, 이미지나 CSS, 동적으로 로드되는 스크립트들은 HTML 태그를 통해서 원본에 접근할 수 있습니다. 크로스 사이트 위조 공격은 same origin policy가 HTML 태그에 적용되지 않는다는 점을 이용합니다.
