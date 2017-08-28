---
title: Gitbook PDF 설정 (book.json)
categories: Gitbook
---

팀프로젝트 완료 일정이 늦어진 관계로 하이어링데이에 작업 결과물을 보여줄 수가 없게 되었다.

우리 Backend가 작성한 100페이지가 넘는 방대한 API 문서는 애증의 gitbook에 작성했기 때문에 하이어링데이 장소의 네트워크가 좋다고 해도 믿을 수가 없다.

< 애증의 gitbook - 1277초만에 Update에 성공했다며 축하 메일을 보내왔다. >
![gitbook-class](/../../../../../images/gitbook-class.png)

<br>

고민을 하다가 결국 API 문서를 출력해서 가지고 가기로 결정했다!

<br>

문서라는 것이 아날로그로 출력을 하고 나면 틀린 부분을 고칠 수가 없기때문에 한번 훓어보고 PDF로 다운받아 출력하는 것이 좋겠다고 생각했다. (날밤의 시작)

```
gitbook 수정 -> gitbook 업데이트 끝날때까지 기다림 -> pdf 다운로드 -> 확인 -> 문제점 찾아 조사
```

이 과정을 무한 반복....-_-;; (로컬에서 하면 그나마 줄어들긴 함. [로컬에서 작업하는 방법](http://recordingbetter.com/gitbook/2017/08/24/Gitbook-Update_local%EC%97%90%EC%84%9C-%EC%9E%91%EC%84%B1,-pdf-%EC%B6%9C%EB%A0%A5.html))

<br>

![gitbook-class](/../../../../../images/gitbook-pdf-button.png)

book의 최초 화면에서 저 버튼을 클릭하면 렌더링 되어있던 pdf를 다운받는다.

다운받아보니 글자가 엄청 커서 120페이지가 넘어가고, 가로로 긴 표는 짤리고... 
내용도 아직도 고칠 것들이 있었다. 

pdf 셋팅을 어디서 해야하는지.....
gitbook 문서, 중국어 블로그, 일본어 블로그, 프랑스어 블로그, npmjs.com까지 뒤져서 알아낸 방법을 정리하면...(구글신 만세, 공통적으로 gitbook을 사용하면서 인내심이 필요하다고 하고 있음 ㅋㅋ)


### book.json

```json
{
	// 현재 문서에서 사용할 플러그인들
	"plugins": [ "theme-api", "hide-published-with", "multipart" ],
	// 그 플러그인들의 셋팅..
	"pluginsConfig": {
		"theme-api": {
			"languages": [
				{
					"lang": "js",
					"name": "JavaScript",
					"default": true
				},
				{
					"lang": "go",
					"name": "Go"
				}
			]
		}
	},
	
	// 현재 문서의 타이틀. 웹에서 setting에서도 정해줄 수 있음.
	// description, authors, isbn, lanhuage 등..
	"title": "Picky Cookbook API Document",
	
	// 현재 문서에 추가할 링크
	"links": {
		// 링크를 추가할 위치. 왼쪽 상단에 나온다.
		"sidebar": {
			// 보여줄 링크 이름: 링크
			"Warp to Picky Cookbook Site": "https://pickycookbook.co.kr",
			"Warp to Github": "https://github.com/fc-pickyeater/wps-picky"
		}
	},
	
	// css 적용 가능하다.
	"styles": {
	    "website": "styles/website.css",
	    "ebook": "styles/ebook.css",
	    "pdf": "styles/pdf.css",
	    "mobi": "styles/mobi.css",
	    "epub": "styles/epub.css"
	},
	
	// pdf 옵션
	"pdf": {
	
		// font size. 기본은 12
		"fontSize": 9,
		
		// paper size. 기본이 a4이므로 딱히 써주지 않아도 됨.
		"paperSize": "a4",
		
		// font를 정해줄 수 있다. 하지만 난 안썼음..
		"fontFamily": [폰트 이름],
		
		// chapter가 바꿜때 어떻게 할건지..
		// 가능한 옵션 : pagebreak,rule,both,none
		"chapterMark": "both"
		
		
		// 페이지 여백 설정. 1인치가 72 
		"margin": {
			"right": 42,
			"left": 42,
			"top": 56,
			"bottom": 56
		},
		
		// 페이지 위, 아래에 보일 값 선택 (적용되지 않음. 아래에 추가 설명)
		"headerTemplate": "_TITLE_",
		"footerTemplate": "_SECTION_"
	}
}
```

### 플러그인

1) book.json 파일의 plugins 리스트에 사용할 플러그인 추가


2) gitbook install 하면 적용된다. 
	- 확인 결과, 웹에서는 업데이트하면서 플러그인들을 설치하기 때문에 필요없는 과정.. 로컬에서 작업한다면 해야한다.

```
$ gitbook install
```

3) 플러그인에 설정이 필요할 경우 "pluginsConfig"에 추가

참고) [플러그인 종류](https://plugins.gitbook.com/)는 엄청 많다...


### pdf.header, footer

- 여러 옵션이 있는데 아무것도 적용되지 않음.
- 검색을 해보니 gitbook에 문제가 있는 것 같다.
- [이슈](https://github.com/GitbookIO/gitbook/issues/1718)가 2월에 열려있는데 진행이 안되고 있음. 근데 저 내용대로 바꿔봐도 pdf에 적용되지 않음..