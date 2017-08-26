---
title: Cloudflare에서 AWS Route 53으로 갈아타기
categories: AWS
---

블로그와 팀프로젝트에 각각 도메인을 가지고 있는데 지금까지는 CloudFlare의 네임서버를 사용하고 있었다. 하지만 너무 느리기도 하고 선생님이 바꿔야 된다고 언급하신 것이 기억나서 검색을 해보니....
  
CloudFlare는 TTFB(Time To First Byte)가 느리다고 한다. 
이게 느리면 구글에서 검색 결과에도 노출시켜주지 않는다고....
[출처](https://hackya.com/kr/%ED%81%B4%EB%9D%BC%EC%9A%B0%EB%93%9C%ED%94%8C%EB%A0%88%EC%96%B4-cloudflare-%EB%A5%BC-%EC%93%B0%EC%A7%80-%EB%A7%90%EC%95%84%EC%95%BC-%ED%95%98%EB%8A%94%EC%9D%B4%EC%9C%A0/)
  
게다가 대한민국 회선의 가격이 비싸다는 이유로 LAX(미국 캘리포니아 LA)쪽으로 연결한다.
[출처](https://namu.wiki/w/Cloudflare#fn-3)
  
팀프로젝트의 경우 AWS Seoul Region을 사용하고 있는데 왜 미국까지....
어쩐지 겁나 느려... AWS 프리티어 박대하는줄...
  
그래서 AWS Route 53으로 갈아타보기로 했다.
  
[AWS Route 53 공식문서](http://docs.aws.amazon.com/ko_kr/Route53/latest/DeveloperGuide/Welcome.html)
  
공식문서는 언제나처럼 겁나많고 결정적인 도움이 되진 않는다....

### 1. Hosted Zone 만들기

- Route 53 서비스를 시작하고 `Hosted Zones`에서 `Create Hosted Zone`을 선택
- Domain Name은 현재 소유하고 있는 도메인의 루트도메인을 적는다. (ex. `recordingbetter.com`)
- Comment는 원하는대로...
- Type은 `Public Hosted Zone`, `Private Hosted Zone for Amazon VPC` 2가지가 있는데 `Private Hosted Zone for Amazon VPC`은 VPC끼리만 트래픽이 라우팅되므로 아무 이름이나 선택할 수 있지만 외부에서는 액세스가 되지 않는다. 나는 DNS를 사용할 것이라 `Public Hosted Zone` 선택.
- 아래 `Create` 클릭하여 Hosted Zone을 만든다.

### 2. Name Server 설정

- 처음 화면에 `NS` 레코드와 `SOA` 레코드가 이미 만들어져있다.
- Domain을 만든 사이트로 넘어가 Name Server를 Route 53 Hosted Zone의 `NS`에 있는 값들로 바꿔준다.
- Name Server 변경이 적용되는데 걸리는 시간은 그때그때 달랐다. (이번엔 5초, 지난번엔 5시간..)

### 3. 메인 도메인의 레코드 설정 (AWS EB일 경우)

- CloudFlare에서는 메인 도메인 주소를 `CNAME`으로 지정하면 에러가 떠도 되긴 되었는데 Route 53에서는 되지 않았다..
- `Create Record Set`을 클릭
- 메인도메인이므로 `Name`은 비우고, `Type`에서 `A`를 선택한다.
- AWS Elastic Beanstalk으로 보낼거라 `Alias`는 Yes, Target은 EB 주소를 입력한다.
- Route Policy는 특별한 것이 없으므로 `Simple`
- `Save Record Set`

## 4. 메인 도메인의 레코드 설정 (AWS EB가 아닐 경우)

- `Create Record Set`을 클릭
- 메인도메인이므로 `Name`은 비우고, `Type`에서 `A`를 선택한다.
- `Alias`는 No, Value에 타겟도메인의 IP 주소를 입력한다.
- IP 주소는 검색하여 나오는 사이트에서 찾을 수 있다. (site IP 등..)
- Route Policy는 특별한 것이 없으므로 `Simple`
- `Save Record Set`

## 5. 서브 도메인의 레코드 설정

- `Create Record Set`을 클릭
- `Name`에 서브도메인 입력
- `Type`에서 `CNAME`를 선택한다.
- `Alias`는 No, `Value`에 연결할 도메인 주소를 쓰면 된다. 
