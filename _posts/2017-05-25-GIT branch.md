---
title: GIT Branch
slug: "git branch"
layout: post
categories: GIT
---


## Git 브랜치

- 버전의 가지
- 협업을 하기위해필수

#### 브랜치 만들기

```
$ git branch [이름]
$ git branch -v 					// 브랜치 리스트 확인
$ git checkout -b [브랜치이름]	// 브랜피를 만들고 그 브랜치로 이동

```

- 브랜치는 커밋을 가르킴
- 태그도 브랜치와 같이 커밋을 가르킴.
- 커밋은 스냅샷을 가르킴.
- 스냅샷은 blob의 데이터를 가지고 있음

#### 작업 브랜치 변경

```
$ git checkout [브랜치이름]
```

- 브랜치를 변경하면 해당 브랜치가 가지고 있는 커밋으로 이동.
- 해당 브랜치가 가지고 있는 커밋 버전으로 로컬 파일이 바뀜

#### 브랜치 이름 변경

```
$ git branch - [기존이름] [새이름]
```


## Merge

```
$ git merge hotfix
```

- 현재 브랜치에 hotfix의 변경 내용을 merge
- production에서 $ git merge hotfix 하면 hotfix가 production으로 합쳐짐

#### 브랜치 삭제

```
$ git branch -d [삭제할 브랜치]
```

#### 파일 충돌 conflict

__같은 파일이 수정된 브랜치를 merge할 경우, 해당 파일을 수정하라고 메세지가 뜨며, 파일 내부에 브랜치 별 내용을 구분해놓음.__

`$ git status` 충돌이 일어난 내용 확인.
해당 파일 내용을 정리한 뒤에 `$ git add` 후 `$ git commit` 하면 merge 됨.

#### fetch / pull

- fetch 리모트에 있는 내용을 로컬로 받아옴. 로컬과 merge 하지 않음
- pull 리모트에 있는 내용을 로컬로 받아오면서 merge 작업까지 함.


```
$ git push origin serverfix:serverfix
```

- “로컬의 serverfix 브랜치를 리모트 저장소의 serverfix 브랜치로 Push 하라” 라는 뜻이다.

#### 리모트에서 브랜치 삭제
```
$ git push origin --delete serverfix
```

## rebase

- 브랜치를 합쳐줌. merge랑은 다름.
- **이미 공개 저장소에 Push 한 커밋을 Rebase 하지 마라**
- [https://git-scm.com/book/ko/v2/Git-브랜치-Rebase-하기]()

