---
title: GIT Tracking etc
slug: "GIT Tracking etc"
layout: post
categories: GIT
---

## 브랜치 추적

- 리모트 트래킹 브랜치를 로컬 브랜치로 Checkout 하면 자동으로 "트래킹(Tracking) 브랜치"가 만들어진다 (트래킹 하는 대상 브랜치를 "Upstream 브랜치" 라고 부른다). 트래킹 브랜치는 리모트 브랜치와 직접적인 연결고리가 있는 로컬 브랜치이다. 트래킹 브랜치에서 git pull 명령을 내리면 리모트 저장소로부터 데이터를 내려받아 연결된 리모트 브랜치와 자동으로 Merge 한다.

- 서버로부터 저장소를 Clone을 하면 Git은 자동으로 master 브랜치를 `origin/master` 브랜치의 트래킹 브랜치로 만든다. 트래킹 브랜치를 직접 만들 수 있는데 리모트를 `origin`이 아닌 다른 리모트로 할 수도 있고, 브랜치도 `master`가 아닌 다른 브랜치로 추적하게 할 수 있다. `git checkout -b [branch] [remotename]/[branch]` 명령으로 간단히 트래킹 브랜치를 만들 수 있다. `--track` 옵션을 사용하여 로컬 브랜치 이름을 자동으로 생성할 수 있다.

```
$ git checkout --track origin/serverfix

Branch serverfix set up to track remote branch serverfix from origin.
Switched to a new branch 'serverfix'
```

- 이 명령은 매우 자주 쓰여서 더 생략할 수 있다. 입력한 브랜치가 있는 (a) 리모트가 딱 하나 있고 (b) 로컬에는 없으면 Git은 트래킹 브랜치를 만들어 준다.

```
$ git checkout serverfix

Branch serverfix set up to track remote branch serverfix from origin.
Switched to a new branch 'serverfix'
```

- 리모트 브랜치와 다른 이름으로 브랜치를 만들려면 로컬 브랜치의 이름을 아래와 같이 다르게 지정한다.

```
$ git checkout -b sf origin/serverfix

Branch sf set up to track remote branch serverfix from origin.
Switched to a new branch 'sf'
```

- 이제 sf 브랜치에서 Push 나 Pull 하면 자동으로 `origin/serverfix`로 데이터를 보내거나 가져온다.

이미 로컬에 존재하는 브랜치가 리모트의 특정 브랜치를 추적하게 하려면 git branch 명령에 `-u`나 `--set-upstream-to` 옵션을 붙여서 아래와 같이 설정한다.

```
$ git branch -u origin/serverfix

Branch serverfix set up to track remote branch serverfix from origin.
```

### subtree / submodule

### getrrit code review

- 코드 리뷰 사이트.
- 안드로이드 프로젝트가 사용 중
- 대기업에들 사용한다
- 서브밋

### hooks

- commit 등 특정 이벤트에 자동으로 실행되는 스크립트
- .git 폴더에 샘플들이 들어있음. 사용시 .sample 삭제

### 코드 작성, 수정 완료 후

```
$ git fetch
$ git merge origin master

# 여기에서 conflict를 잡아주고 가야함. 없으면 이득
# 그리고 반드시 테스트!!!

$ git push
```

### redis

- 메모리 db
- 파일시스템을 사용하지 않아 빠르다
- 세션 관리할때 사용
