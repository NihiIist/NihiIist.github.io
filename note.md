---
layout: page
title: "y"
---

# jekyll
* 서버 실행
> bundle exec jekyll serve

# git
* 브랜치 모든 커밋 하나의 커밋으로 병합 후 가져오기
> git merge --squash 'branch'
* 브랜치 생성 + checkout
> git checkout -b 'branch'
* remote 브랜치 갱신
> git remote udpate

* local git ignore
    - .git/info/exclude 에 파일 추가

# ant design
* spin
    * spin으로 감싸도 component들 렌더링 됨. loading될 때까지 tip으로 가려주는 역할.
    * get요청을 보내는 component가 하위에 있는 경우에 유의.