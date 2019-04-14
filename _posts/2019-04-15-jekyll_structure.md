---
layout: post
title: jekyll 폴더 구조 살펴보기
permalink: posts/jekyll-structure
tag: javascript jekyll github githubpage theme
---

> 해당 포스트는 [Jekyll File Structure](https://medium.com/@r3id/jekyll-file-structure-f28c496f8dc0)를 번역하여 작성하였습니다. 잘못된 부분이 있다면 댓글 부탁드립니다.

이 포스팅에서 지킬에서 디렉토리가 의미하는 바가 무엇인지 개괄적으로 살펴볼 예정입니다. 이 컨셉을 잘모르더라도 걱정하지 마세요. 글을 읽은 후에는 파일과 디렉토리가 의미하는 바를 이해할 수 있을 겁니다.

![jekyll directory](https://cdn-images-1.medium.com/max/1600/1*ZVopl3AWtULTpuIoNRGRyQ.png)

## \_config.yml

\_config.yml파일은 지킬 사이트의 환경설정을 포함하고 있고 흔히 아래와 같은 방법으로 사용합니다.

- 사이트 전체에서 사용하는 변수를 설정합니다.
- 디폴트 값을 설정합니다.
- 매번 실행할 런타임 변수를 지정합니다.

## \_posts

\_posts 폴더는 블로그 글이 저장되어 있는 곳입니다.

포스트 파일의 네이밍 컨벤션은 매우 중요하고 `년도-월-일-제목.md`의 포멧을 따라야 합니다. permalinks는 포스트마다 다르게 할 수 있지만 날짜와 마크업 언어는 파일이름에 의해서 결정됩니다.

## \_site

\_site는 컴파일된 HTML파일이 저장되는 장소입니다. 일단 빌트하면 파일들은 호스팅을 위해 서버에 직접 업로드됩니다. 보통 [github pages](https://pages.github.com/)를 추천합니다.

git을 사용할 때 팁은 .gitignore파일을 사용해 컴파일된 \_site 폴더가 업로드되지 않게 하는 것입니다.

## Pages

아마 index.md와 about.md 파일이 있다는 것을 확인했을 겁니다. 이 파일들은 마크다운 파일이고 지킬에서 해당 파일을 가지고 여러 작업을 할 수 있습니다. 마크다운에 대해서는 다음 포스팅에서 언급하겠습니다.

각 파일 최상위에서 페이지에대한 몇 가지를 결정해야합니다. 이것이 각 페이지를 만들 때 참조하는 것들입니다. 이것들을 활용해서 홈페이지를 다양하게 수정할 수 있지만 기본적인 레벨에서 아래 내용을 참고하시면 됩니다.

- layout: 페이지에서 사용할 레이아웃
- title: 페이지 타이틀
- permalink: 페이지의 permalink

여기에 index.html 파일 맨 위에 추가할 수 있는 예시가 있습니다.

홈페이지 세팅이 되어 있다면 지금 당장 콘텐츠를 추가해야합니다. 간단하게 페이지에 나타낼 HTML파일을 추가하면 됩니다.
