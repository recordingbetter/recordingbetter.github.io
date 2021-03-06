---
title: GIT Try Out
slug: "git try out"
layout: post
categories: GIT
---

## GIT 최초 설정

1. `/etc/gitconfig` 파일: 시스템의 모든 사용자와 모든 저장소에 적용되는 설정이다. `git config --system` 옵션으로 이 파일을 읽고 쓸 수 있다.

2. `~/.gitconfig`, `~/.config/git/config` 파일: 특정 사용자에게만 적용되는 설정이다. `git config --global` 옵션으로 이 파일을 읽고 쓸 수 있다.

3. `.git/config`: 이 파일은 Git 디렉토리에 있고 특정 저장소(혹은 현재 작업 중인 프로젝트)에만 적용된다

#### 사용자 정보 설정

- 최초 한번만 설정하면 됨

```terminal
$ git config --global user.name "이름"
$ git config --global user.email "이메일"
```

#### 편집기 설정

```
$ git config --global core.editor emacs
```

#### 설정 확인

```
$ git config --list
```

#### 도움말 (오프라인 가능)

```
$ git help
```

## GIT 저장소 만들기 (로컬)

#### Index / Working Tree

- Index : 새 커밋이 되기 직전의 단계 (stage area)
- Working Tree : 현재 작업하고 있는 파일

#### 버전 관리할 디렉토리에서 git 저장소를 만들고 초기화

```
$ git init
```

#### 디렉토리에 추가된 파일을 git 저장소에 추가

```
$ git add [file name]
```

#### git 상태 확인

```
$ git status
```

버전 관리 중인 디렉토리의 파일들의 상태를 보여줌.

#### 파일의 상태

- Untracked : 버전관리에 제외되어있는 파일 $ git add [file name]으로 추가하면 Staged 상태가 된다.
- Unmodified : 버전관리 중(Tracked)이며 이전 commit과 비교하여 수정이 되지 않은 파일
- Modified : 버전관리 중(Tracked)이며 이전 commit과 비교하여 수정된 파일
- Staged : Tracked 파일 중, Modified 파일을 commit 하기 위해 Staged 상대로 만든다.

#### 버전 관리에 제외할 파일 리스트 .gitignore

```
vim .gitignore
```

- commit에서 제외할 파일의 리스트를 작성한다. (패턴으로 작성 가능)
	- 아무것도 없는 라인이나, `#`로 시작하는 라인은 무시한다.
	- 표준 Glob 패턴을 사용한다.
	- 슬래시(/)로 시작하면 하위 디렉토리에 적용되지(Recursivity) 않는다.
	- 디렉토리는 슬래시(/)를 끝에 사용하는 것으로 표현한다.
	- 느낌표(!)로 시작하는 패턴의 파일은 무시하지 않는다.
	- * 는 하나도 없거나 모든 문자.
	- ** 아무 디렉토리
	- [abc] 는 a, b, c 중 1개의 문자
	- [0-9] 숫자 1개
- https://www.gitignore.io 에서 `macOS`로 생성하여 붙여넣기 해도 됨

#### modified, not staged files

```
$ git diff
```

#### Staging Area

```
$ git diff --staged //or
$ git diff --cached
```

#### COMMIT!

```
$ git commit
```

Leave commit message on vim editor.

```
$ git commit -m "commit message"
```

#### Staging 과정 생략하기

```
$ git commit -a
```

tracked file을 자동으로 staging area에 넣어준다.

#### 파일 삭제 rm

```
$ git rm [file name]
```

tracked file을 삭제(staging area에서 삭제)한 뒤에 commit 해야 함.
삭제할 파일이 staging area에 있다면 `-f` 옵션으로 강제 삭제

#### 파일 이름 변경 mv

```
$ git mv [from name] [to name]
```
commit 하지 않아도 됨

#### git log

```
$ git log				//로그 확인
$ git log -p			//자세한 로그 확인
$ git log -3			//최근 3개의 커밋로그만 확인
$ git log --oneline	//각 로그를 1줄씩
$ git log --graph	//브랜치를 그래프로
$ git log --all		//전체 로그 확
$ git log --decorate //브랜치 보이게
$ git log --oneling --graph --decorate --all //완성형

$ git config --global alias.adog "log --all --decorate --oneline --graph"		// git adog 명령으로 완성형 입력

```

#### 버전 되돌리기

```
$ git commit --amend //직전 커밋 내용에 덮어쓴다.
$ git checkout [체크섬의 처음 일부문자]	//로컬 파일을 이전 버전으로

```

#### 파일을 unstaged로 변경

```
$ git reset HEAD [file name]
```

#### modified 파일 되돌리기

```
$ git checkout -- [file name]
```
수정하기 전으로 되돌림 (위험..)

## 리모트 저장소

#### 리모트 저장소 확인

```
$ git remote //or
$ git remote -v
$ git remote show [리모트 저장소 단축이름]
```

#### 리모트 저장소 추가 add

먼저 github 등에 저장소를 만든다. (url 복사)

```
$ git remote add [리모트 저장소 단축이름] [url]
```

#### 리모트 저장소에 파일 복사 push

```
$ git push origin master
$ git push [리모트 저장소 단축이름] [브랜치]
```

#### 기존 저장소를 복사 clone

- 리모트, 로컬 모두 가능

```
$ git clone [url] [생성할 드렉토리이름]
```

#### fork / clone / pull request

- 리모트 저장소를 fork하면 리모트에 저장소가 생긴다.
- 그 리모트 저장소를 clone하면 로컬에 저장소가 생긴다.
- pull하면 clone했던 리모트 저장소에 업데이트된다.
- 원본에 push를 하고 싶으면 pull request 한다.

#### 리모트 저장소 이름 바꾸기 rename

```
$ git remote rename [기존이름] [새이름]
```

#### 리모트 저장소 삭제 rm

```
$ git remote rm [리모트 저장소 단축이름]
```

#### tag

- lightweight tag : 최슨 커밋으로 이동하지 않음. 특정 커밋을 가르킴.
- annotated tag : 태그를 만든 사람 이름, 이메일 메세지 등을 저장. `-a`


```
$ git tag -a [태그이름] -m "메세지" 	//annotated tag
$ git tag [태그이름] 					//lightweight tag
```

```
$ git push origin v1.0
$ git push origin --tags			//여러개의 태그 푸시
```

- 태깅 후에 푸시. 그냥 푸시로는 안됨.
- 저장소(github)의 release 리스트에 있음. 링크 제공
