---
layout: post
title: 모던 웹 브라우저의 이해
permalink: posts/jekyllLocalServer
tag: githubPage jekyll
---

블로그를 거의... 1년만에 다시 시작했다. 회사에 적응하면 해야지 했던 나의 다짐은 다짐으로만...   

무튼 오랜만에 포스팅을 하면서 `jekyll` 로컬 서버로 돌려보려고 했는데 `README.md` 파일에 따로 설치하는 방법을 남겨놓지 않았다ㅠㅠ

구글링으로 찾으면 금방하겠지라는 생각으로 검색을 했다.

그래서 빠르게 [Jekyll on macOS](https://jekyllrb.com/docs/installation/macos/) 튜오리얼을 찾았다.

처음부터 차근차근 읽어보면서 설치를 하고 있는데 아래 명령어를 입력하는데 `ruby` 버전이 2.4.0 이상에서만 `jekyll`이 설치된다는 오류 메세지가 떴다. 

    gem install --user-install bundler jekyll

그래서 `ruby`와 `ruby` 버전 매니저인 `rbenv`도 삭제하고 다시 설치하면 되겠지하고 재 설치를 했다.

그런데... `ruby` 버전이 2.3.7에서 업데이트가 되지 않았다. 뭐지...

하면서 여기서부터 삽질이 들어갔다.

`rbenv`에서 ruby 버전을 올려보고, 구글링으로 온갖 스택오브플로우는 다 찾아본 것 같다.

그러다가 그러다가 `brew list` 으로 `brew`설치 된 패키지를 확인했는데 거기에 `ruby-build`가 설치되어 있는 걸 확인했다.

설마..가 역시나.. `ruby-build`를 지우고 튜토리얼대로 설치를 하니 `jekyll`은 정상적으로 깔렸다!!

삽질은 했어도 그래도 로컬서버에서 잘 돌아가니 기분은 좋았다.

