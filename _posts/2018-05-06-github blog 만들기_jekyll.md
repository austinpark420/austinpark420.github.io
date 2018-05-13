---
layout: post
title: github blog 만들기_jekyll
permalink: posts/githubblogsetting_jekyll
tag: jekyll blog github pages
---
1. github blog repo만들기

2. github blog repo clone 하기

```
// path: Documents/dev
// path is located whenever you want

$ git clone https://github.com/username/username.github.io
```

3. index.html 파일 만들기

```
// path: Documents/dev/username.github.io

$ echo "Hello World" > index.html
```

4. github repo에 add, commit, push 하기

```
// path: Documents/dev/username.github.io

$ git add --all
$ git commit -m "Initial commit"
$ git push -u origin master
```

5. ruby install 여부확인

```
// path: Documents/dev/username.github.io

$ ruby --version
```

6. ruby 설치하기

```
// brew 활용하기

$ brew install ruby
```

7. .Gemfile 생성

```
// path: Documents/dev/username.github.io

$ touch Gemfile
```

8. bundle install

```
// path: Documents/dev/username.github.io

$ bundle install
// Fetching gem metadata from https://rubygems.org/............
// Fetching version metadata from https://rubygems.org/...
// Fetching dependency metadata from https://rubygems.org/..
// Resolving dependencies...
```

9. 테마적용하기
[jekyll theme](http://jekyllthemes.org/)

### 참고

  * github blog repo만들기 [github page](https://pages.github.com/)
  * jekylle 설치 [github help](https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/)
  * theme 적용 [jekyll theme](http://jekyllthemes.org/)
  * url path 설정 [permalink](https://jekyllrb.com/docs/permalinks/#permalink-style-examples)