---
layout: post
title: Homebrew와 NPM(macOS x)의 차이점
permalink: posts/homebrew-npm
tag: homebrew npm macos
---

> 해당 포스트는 [What is the difference between Homebrew and NPM (macOS X)?](https://www.quora.com/What-is-the-difference-between-Homebrew-and-NPM-macOS-X)를 번역하여 작성하였습니다. 잘못된 부분이 있다면 댓글 부탁드립니다.

정확하지 않은 정답일 수 있지만 굉장히 쉽게 homebrew와 npm에 대해서 이해할 수 있는 내용은 아래와 같습니다.

- Homebrew는 맥 앱스토어와 같습니다. 소프트웨어를 인스톨하면 모든 시스템에서 사용할 수 있습니다.
- npm은 크롬의 확장 프로그램같습니다. 하나의 어프리케이션 안에서만 기능이 동작합니다.

---

homebrew는 소프트웨어를 탐색하고 설치하고 삭제하고 업데이트하는 관리 툴입니다. 이것은 Github 레포지터리에 기반을 둔 서비스이고 소스코드를 다운로드, 컴파일, POSIX 유틸기반의 의존성 컴포넌트틀 처리하기 쉽게 했습니다. 또한 /usr/local 디렉토리 안에 위치했습니다. Homebrew를 통해 인스톨한 소프트웨어는 유저 스페이스 프로세스에서 독립적입니다. 대부분의 유틸리티는 터미널에서 실행되는 cli기반 툴입니다.

npm은 Node.js의 패키지 관리 툴입니다. Node.js는 Java나 PHP와 비슷하게 런타임환경에서 동작합니다. 이것은 javascript로 작성되었지만 브라우저밖에서 실행될 수 있고 다른 프로세서와 상호작용할 수 있고 웹서버를 위한 CGI같이 자바스크립트 코드를 처리할 수 있습니다. npm으로 인스톨한 패키지 소프트웨어는 소스코드 라이브러리 혹은 Node.js 환경에서만 동작하는 확장프로그램입니다. 만약 자바스크립트 소스코드가 영어를 프랑스어로 변환하는 구글번역 서비스같은 확장 기능을 실행한다면 Node.js에 패키지가 설치됩니다. 그렇지 않으면 자바스크립트 코드는 실행되지 않습니다.
