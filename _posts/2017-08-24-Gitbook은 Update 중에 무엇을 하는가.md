---
title: Gitbook Update / local에서 작성, pdf 출력
categories: Gitbook
---

< 애증의 gitbook - 1277초만에 Update에 성공했다며 축하 메일을 보내왔다. >
![gitbook-class](/../../../../../images/gitbook-class.png)

<br>

### gitbook에서 `update`는 저장이 아니다.

웹브라우저에서 gitbook -> edit 해서 작성하는 부분은 github에서 커밋 내용을 수정하는 것과 마찬가지의 과정이다. 그런데 여기서 오른쪽 상단에 `Publish` 버튼이 있는데 단축키로 `커맨드 + S`.
  
마치 `저장` 버튼인척 하고 있는 이 버튼을 클릭하면 작성중인 gitbook의 가장 첫 화면에서 볼 수 있는 `UPDATES`에 커밋이 하나 생기면서 update 중이라며 빙글빙글 돌고 있다.
  
이 상황에서는 `read` 모드에서나, 다른 작성자의 웹브라우저 edit 화면에 나의 변경 사항이 적용되지 않는다. 근데 이 상황이 짧게는 십여초, 길게는 몇시간까지 가는 것이 문제다.
재미있는 것이 이 상황에서도 터미널에서 git pull을 하여 확인해보면 변경 사항이 아주 잘 적용되어 있다.
  
**`Update`라는 과정은 내가 웹브라우저의 gitbook editor에서 수정한 내용으로 website, json, pdf, mobi, epub 파일들을 모두 다시 렌더링하는 과정이다.**

book 설정 메뉴 중 SETTINGS에서 E-Books를 사용할지 여부를 선택하는 부분이 있다. 여기서 해제를 하면 update 시, website, json만 렌더링 한다. (빨라진다고 한 적은 없다. 그냥 과정이 줄어든다..)
안타깝게도 PDF만 선택하거나 할 수는 없다.
하지만 PDF 파일이 필요하여 다시 E-Books을 선택한다면 선택한것 만으로도 저 5가지를 모두다 다시 렌더링한다. ㅋㅋㅋ
  
렌더링 중에 다른 요청이 오면 그냥 쌓아놓는다. 어차피 소스 자체는 수정이 바로 되어 있고 렌더링만 쌓아놓고 나중에 진행하는데, editor에서는 렝더링이 완료되지 않으면 변경 사항을 알 수가 없기에 그냥 속만 터지는거....
  

  <br>
  
### local에서 gitbook 작성

- gitbook은 git base이기 때문에 사실 git과 버전 관리 방법이 거의 흡사하다.

#### 1. 작성 중인 book을 local에 클론 받는다. (웹에서 작성 중인 book이 있을 경우)

![clone](/../../../../../images/gitbook-clone.png)

```
$ git clone [gitbook 주소] [대상 폴더]
```

- 마크다운으로 작성할 수 있음

#### 2. gitbook cli 설치

- NodeJS 4.0 이상이 설치되어 있어야 함.

```
$ npm install gitbook-cli -g

// gitbook 명령어 확인
$ gitbook help
```

#### 3. local server 실행

```
$ gitbook serve
```

- 웹브라우저에서 localhost:4000으로 확인할 수 있다.

#### gitbook 작성이 완료되면 

- git과 같음

```
$ git add .

$ git commit -m "commit message"

$ git push origin master
```

<br>

### local에서 build

```
$ gitbook build
```

- build 하면 `_book` 폴더가 생성되고 작성한 마크다운 파일들이 html 파일들로 렌더링된다.
- book.json, 플러그인, css 등이 어떻게 적용되는지 확인할 수 있다.

<br>

### local에서 pdf 렌더링

- local에서 작성한 gitbook을 local에서 pdf로 렌더링 해볼 수 있다. (항암효과)

#### 1. ebook-convert 설치

- https://calibre-ebook.com 에서 `calibre`라는 앱을 설치한다.
- 이 앱을 쓸건 아니고 앱에 포함된 cli 명령어를 사용한다.

```
ln -s /Applications/calibre.app/Contents/MacOS/ebook-convert /usr/local/bin
```

- ebook-convert command가 앱 패키지 안에 숨어 있으므로 링크로 꺼내줌.

#### 2. pdf 렌더링

```
// gitbook 폴더에서
$ gitbook pdf 

// 또는
$ gitbook pdf [book] [output]
```

- output을 따로 정하지 않았다면 `book.pdf`로 생성된다.




  
  



