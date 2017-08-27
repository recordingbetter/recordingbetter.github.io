

- 웹을 위한 인터프리터 언어이자 스크립트 언어
- 자바스크립트로 작성된 프로그램을 스크립트라고 부른다.
- 컴프일이 필요하지 않음
- HTML 소스 중간에 삽입할 수 있다.
- 클라이언트의 웹브라우저에서 실행된다.

## Javascript의 역할

- 웹페이지에 기능을 더해 HTML 웹페이지를 동적으로 만들어준다.

1. HTML 페이지 변경 및 엘리먼트, 콘텐츠의 추가/제거
2. CSS, HTML 엘리먼트의 스타닝 변경
3. 사용자와의 상호작용
4. 폼의 유효성 검증
5. 마우스, 키보드 이벤트에 대한 스크립트 실행
6. 웹브라우저 제어
7. 쿠키 등에 대한 설정과 조회
8. AJAX 기술을 이용한 웹 서버와의 통신

## Javascript의 한계

- 일부 보안상의 제약이 있다.
- OS에 직접 접근할 수 없다
- 하드디스크를 읽거나 쓸 수 없다.
- 다른 프로그램을 호출할 수 없다.
- 탭/윈도우 간의 통신을 수행할 수 없다.(같은 도메인일 경우 가능)
- 자체 도메인에 대해서만 제약없이 네트워크 요청을 보낼 수 있다.

#### Javascript 샘플

```javascript
<!DOCTYPE html>
<html>
<head>
<title>JavaScript Hello World</title>
</head>
<body>
 
<script type="text/javascript">
    document.write("Hello, World! This is my first JavaScript.");
</script>
 
</body>
</html>


// 한 줄 주석을 이용해 아래 코드를 설명한다
/*
    자바스크립트 여러 줄 주석 예제:
    첫 번째 줄...
    두 번째 줄... 
*/
```

## 자료형

### 기본 자료형

- 문자열 : 자바스크립트 내의 텍스트를 표현하며, 문자열은 유니코드 문자의 나열이다.
- 숫자 : 모든 숫자(정수와 부동 소수점 수 모두)는 Number 타입이다.
- boolean : 참(true)과 거짓(false)

### 복합 자료형

- 객체 : 값의 집합
- 배열 : 순차적인 값의 집합
- 함수 : 실행 가능한 코드가 담긴 특별한 객체

### 특수 자료형

- null : 값이 없을때
- undefined : 값이 할당되지 않은 변수



