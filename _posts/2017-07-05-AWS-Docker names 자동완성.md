---
title: Docker names 자동완성 설정하기
slug: Docker names 자동완성
layout: post
categories: AWS
---

Docker 컨테이너의 이름, 이미지 이름은 랜덤으로 생성되는데 터미널에서 자동완성이 되지않아 불편하다. 자동완성이 되게 해보자.


- zsh completion 설치

```
$ brew install zsh-completion
```

- docker completion 설치

```
$ brew install docker-completion
```

- ~/.zsh/completion/ 폴더를 만들어 파일 복사

```
$ mkdir -p ~/.zsh/completion
$ curl -L https://raw.githubusercontent.com/docker/compose/master/contrib/completion/zsh/_docker-compose > ~/.zsh/completion/_docker-compose
```

- ~/.zshrc에 아래 내용 추가

```
# fpath에 경로 추가
fpath=(~/.zsh/completion $fpath)
# compinit 실행
autoload -Uz compinit && compinit -i
```
- Shell reload
