---
title: Gitbook에 작성한 API 문서 도메인 변경하기
categories: Gitbook
---

팀프로젝트를 진행하며 작성한 API 문서를 좀 더 그럴듯하게 보이고 싶어 도메인 주소를 바꿨다.

<br>

```
https://docs.pickycookbook.co.kr
```
<br>

### 1. Gitbook에서 설정

- gitbook의 book 설정 부분에 `SETTING` 항목이 있다.
- `Domains`에서 사용하고 싶은 도메인을 `Domain for content`에 입력한다.
- `docs.pickycookbook.co.kr`
- `SAVE`

### 2. DNS에서 설정

- `pickycookbook.co.kr` 도메인의 네임서버를 사용하고 있는 Route 53에서
- `CNAME` 레코드 추가
- Alias는 No, Value는 **`www.gitbooks.io`** 

### 3. Gitbook에서 확인

- gitbook의 book 설정 부분에 `SETTING` 항목
- `Domains`에서 아래 그림이 보인다면 성공

![성공](/../../../../../images/gitbook-domain-success.png)


