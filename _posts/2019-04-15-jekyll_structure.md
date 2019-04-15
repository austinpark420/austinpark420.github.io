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

## gemfile and gemfile.lock

gemfile은 루비의 의존성 관리 시스템이고 루비 프로젝트를 실행할 때 필요함 gem 리스트들을 포함하고 있습니다. jekyll 플러그인 설치할 때 주로 gemfile을 사용합니다.

gem은 루비 프로젝트를 포함한 코드의 모음입니다. gemfile은 다른 사람의 코드를 가져와 프로젝트에 사용할 수 있게 합니다. gem은 아래와 같은 기능을 수행합니다.

- 루비 프로젝트를 JSON으로 변환합니다.
- 페이지네이션
- Github와 같은 외부 API와 상호작용

jekyll 자체 jekyll-paginate와 jekyll-feed 같은 jekyll 플러그인을 포함하고 있습니다.

gemfile을 생성하거나 수정할 때 `$ bundle install`을 실행해야하며 그것은 아래와 같이 2가지 일을 실행합니다.

- gemfile.lock 파일이 없다면 파일을 설치합니다. 해당 파일은 자동으로 생성되고 gemfile안에 있는 gem 추가되고 버전이 정해지지 않았더라도 버전이 포함됩니다. gemfile은 다른 개발자와 코드를 공유하도록 보장하며 모두 동일한 gems 버전을 가지고 있습니다.
- gemd은 gemfile.lock에 다운로드 합니다.

## .jekyll-metadata

.jekyll-metadata는 jekyll이 빌드된 후에 수정되지 않은 파일과 다음에 빌딩할 때 재시작해야할 파일을 추적할 수 있습니다. 이 파일은 사이트를 생성된 사이트에 포함되지 않습니다. 이 파일을 .gitignore에 포함하는 것을 추천합니다.

## \_layouts

\_layouts 폴더에는 콘텐츠를 감쌀 템플릿이 포함되어 있습니다. 헤더와 푸터, 네이베이션과 같이 전형적으로 반복되는 코드가 \_layouts안에 포함되어 있습니다.

## \_includes

페이지의 일부분이 포함될 수 있습니다. 포함되어 있는 것들은 일반적으로 뉴스레터 구독폼과 푸터와 같이 중복으로 사용되는 페이지 입니다.

{% raw %} {% include file.ext %} {% endraw %}와 같은 리퀴드 태그는 \_includes / file.ext에 부분을 포함시키는 데 사용할 수 있습니다.

## \_drafts

퍼블리싱 안되 블로그 포스트를 담아놓는 폴더입니다. \_draft폴더는 우리 실제 홈페이지에 퍼블리싱없이 작업할 수 있도록 도와줍니다.

## \_data

\_data는 YAML, JSON, CSV파일을 포함합니다. 이 파일안에 있는데이터는 jekyll 사이트에서 사용될 수 있습니다.

## Other Files/Folders

프론트 문제가 있는 파일들은 실행되어지고 \_site에 출력됩니다. 프론트 문제(HTML, CSS, javascript)가 없다면 \_site에 복제되어 빌드됩니다.
