---
title: GIT Grep Reset
slug: "GIT Grep Reset"
layout: post
categories: GIT
---

## 검색 도구

### git grep

- 커밋트리의 내용, 워킹 디렉토리의 내용을 문자열이나 정규표현식으로 검색할 수 있다.

```
$ git grep -n [검색어]			//검색 결과를 줄 번호와 함께 보여준다.
$ git grep --count [검색어]		//검색 결과의 갯수를 보여줌
$ git grep -p [검색어]			//함수나 메서드를 검색하여 보여줌
$ git grep --and	[검색어]			//한 라인에 검색어가 여러개 있는 줄검색
```

### 로그 검색

- 히스토리에서 언제 추가되거나 변경되었는지 검색

```
$ git log -S [검색어] --oneline		//검색어가 처음 추가된 커밋, 없어진 커밋을 검색
$ git log -G [정규표현식]				//정규표현식으로 검색
$ git log -L :[함수명]:[파일명]		//파일 내에 함수나 라인의 히스토리 검색
```

## 히스토리 단장

- 사람들과 코드(저장소)를 공유하기 전에 commit history 정리해야된다.

#### 마지막 커밋 수정

```
$ git commit --amend				//마지막 커밋 메세지를 수정할 수 있게 열어줌
```
- **rebase와 같이 이미 push한 커밋은 수정하면 안된다.**

#### 커밋 메세지 여러개 수정
- 직전 커밋이 아닌 예전의 커밋 수정
- 개별 커밋을 수정하지 않고 특정 시점부터 현재 위치(HEAD)까지의 커밋을 rebase
- `-i` 옵션으로 대화형 작업 가능 **(log의 순서와 반대로 나온다)**

```
$ git rebase -i HEAD~3				//마지막 커밋 3개를 수정
```

- 커밋 메세지 수정 화면에서 `pick`를 `edit`로 변경하면 그 커밋에서 멈춘다.
- 저장하고 편집기를 종료하면 Git은 목록에 있는 커밋 중에서 가장 오래된 커밋으로 이동
- 이후 설명에 따라, 아래 명령 실행.

```
$ git commit --amend
$ git rebase --continue
```

#### 커밋 순서 바꾸기

- 대화형 rebase 도구로 커밋을 삭제하거나 순서를 조정할 수 있다.

```
pick f7f3f6d changed my name a bit
pick 310154e updated README formatting and added blame
pick a5f4a0d added cat-file
```

커밋 메시지를 아래와 같이 수정하면 `added cas-file` 커밋은 삭제되고 다른 두 커밋은 순서가 바뀐다.

```
pick 310154e updated README formatting and added blame
pick f7f3f6d changed my name a bit
```

#### 커밋 합치기

- 대화형 rebase 도구로 커밋을 합칠 수 있다.
- `pick` 대신 `squash`로 변경하면 해당 커밋과 이전 커밋을 merge 커밋 메세지도 merge

#### 커밋 분리

- 기존의 커밋을 해제하고 stage를 여러개로 분리하고, 다시 커밋.
- 대화형 rebase 도구를 사용

```
pick f7f3f6d changed my name a bit
edit 310154e updated README formatting and added blame
pick a5f4a0d added cat-file
```

커밋 310154e를 2개의 커밋으로 분리하려면,
대화형 rebase 화면에서 해당 커밋을 `edit`로 변경한다.
커밋 해제는 `git reset HEAD^` -> 수정했던 파일들이 unstaged 상태가 된다.
그 다음 파일들을 staged 한 뒤에 원하는만큼 커밋한 뒤, `git rebase --continue`을 실행하면 rebase 작업이 끝난다.

```
$ git reset HEAD^							//커밋해제
$ git add README							//파일 추가1
$ git commit -m 'updated README formatting'	//새로운 커밋1
$ git add lib/simplegit.rb					//파일 추가2
$ git commit -m 'added blame'				//새로운 커밋2
$ git rebase --continue						//rebase 작업 종료
```

결과

```
$ git log -4 --pretty=format:"%h %s"
1c002dd added cat-file						//기존 a5f4a0d
9b29157 added blame							//새로운 커밋2
35cfb2b updated README formatting			//새로운 커밋
f3cc40e changed my name a bit				//기존 f7f3f6d
```

- **이 작업은 커밋의 체크섬을 변경시키므로 remote에 push한 커밋을 수정하면 안된다.**

### filter-branch 수정해야할 커밋이 많은 경우

- push한 이후에는 사용하면 안된다.

##### 모든 커밋에서 특정 파일 삭제

```
$ git filter-branch --tree-filter 'rm -f passwords.txt' HEAD
```

- 모든 파일과 커밋을 정리하고 브랜치 포인터를 복원해준다.
- 테스트 브랜치에서 테스트 후 마스터 브랜치에 적용하는 것이 좋다.
- `--all` 옵션으로 모든 브랜치에 적용 가능

## git reset과 checkout

### reset


##### 트리 : 실제 파일의 묶음

|트리|역할|
|---|---|
|HEAD|마지막 커밋 스냅샷. 다음 커밋의 부모. 현재 브랜치|
|index|다음에 커밋할 스냅샷 (stage)|
|working directiry|샌드박스, 로컬 작업 공간|

##### reset 과정

1. HEAD 이동 : 현재 브랜치가 가리키는 커밋을 변경
	- `$ git reset --soft HEAD~` `--soft` 옵션으로 이 과정에서 멈출 수 있다.

2. index 업데이트 : index를 HEAD가 가리키는 스냅샷으로 업데이트
	- `$ git reset --mixed HEAD~` `--mixed` 옵션으로 이 과정에서 멈출 수 있다. **(reset의 옵션이 생략되면 이 옵션으로 실행된다)**

3. working directory 업데이트 : working directory 파일을 index 내용으로 업데이트 한다.
	- `$ git reset --hard HEAD~` `--hard` 옵션으로 이 과정에서 멈출 수 있다.

##### 경로를 주고 reset

```
$ git reset [커밋 체크섬] [파일이름]		//명시된 커밋에서 파일 스냅샷을 가져온다
```

##### 커밋 합치기

### checkout

- branch 스냅샷을 기준으로 세 트리를 조작한다.
- working directory의 파일이 날아갈 일이 없음.
- working directory에서 merge 작업을 시도 후 변경하지 않은 파일만 업데이트
- **HEAD 자체를 다른 브랜치로 옮김. (cf. reset은 HEAD가 가리키는 브랜치를 변경)**


