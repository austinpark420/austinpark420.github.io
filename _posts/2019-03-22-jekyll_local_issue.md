---
layout: post
title: jekyll 로컬 설치 이슈
permalink: posts/jekyllIssue
tag: [javascript]
---

## jekyll 로컬서버 install 이슈

github 블로그를 jekyll 테마를 사용하고 있다. 기존에 사용하는 컴퓨터말고 다른 컴퓨터에서 포스팅을 하려고 블로그 레포를 클론받고 로컬 서버를 아래와 같은 명령어로 설치하는데

```
$ gem install bundler jekyll
```

계속해서 에러가 났다. 터미널 오류 메세지를 구글에 검색하고 검색된 솔류션을 적용해보았지만 해결책을 못찾았다. 한 2일정도 고생하다가 솔루션을 드디어 문제점을 발견했다. homebrew와 bundle 업데이트가 안되어있어서 나타난 이슈였다. 별거 아닌 것같은데 오래 고생했다... 그래도 해결해서 기분은 좋다.
