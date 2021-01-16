---
layout: post
title: github 충돌나서 겪은 어려움
permalink: posts/githubConflict
tag: github conflict
---

회사 프로젝트를 두명하고 있었는데 잘못된 PR을 develop에서 master로 날려서 revert한 적이 있었다.  
> master - develop - release/{date}으로 branch 관리를 하는데 release/{date} branch에서는 release시기에 맞춰 프로젝트에 참여한 인원이 기능개발을 하고 develop branch에서는 release branch에서 작업한 내용을 합쳐 QA를 진행하고 문제가 없으면 운영상태인 master branch에 PR을 날린다.

그 당시에는 문제가 없다고 생각하고 각자 작업을 진행했다.

문제는 다음 PR을 날릴 때 발생했다.

PR 목록에 파일이 변경된 부분은 내가 수정한 파일 정보들만 나열되여있는데 merge를 하려고하면 6개 정도의 파일에서 충돌이 났다.

지금까지 충돌을 해결했던 방식은 충돌난 파일을 로컬 PC에서 수정을 하고 PR 내용을 수정하는 방식대로 했다.

그런데 이번에는 그런 방식으로 충돌을 해결하려고 하는데 해결이 안됐다. 로컬에서 충돌을 해결하려고 upstream에서 pull 받고 merge를 하기를 여러번..
> 회사 프로젝트를 개인이 fork를 떠서 회사프로젝트 레포를 upstream, 개인이 fork 뜬 레포를 origin으로 사용한다.

하지만 해결되지 않았다.

그래서 다른 개발자 분에게 도움을 청했다. 그분은 master와 develop branch에 commit 내용을 확인하시더니 master에 있는 commit이 develop에는 없다며 master branch의 commit 상태를 develop과 맞춰야한다고 하셨다.

master 코드를 확인해보니 PR날렸을 때 file changed 부분에 표시되었어야 할 내용이 없었다.

그래서 upstream github 레포를 클론받아와 원하는 commit으로 revert 한 다음에 `git fush -f` 명령어를 사용해 강제로 upstream commit 상태를 변경해서 문제를 해결할 수 있었다.




