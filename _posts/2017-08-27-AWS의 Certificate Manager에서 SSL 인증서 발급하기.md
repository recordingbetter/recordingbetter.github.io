---
title: AWS의 Certificate Manager에서 SSL 인증서 발급하기
categories: AWS
---

팀프로젝트의 도메인 네임서버를 AWS Route 53으로 바꿨더니 http로는 접근이 되는데 https로 접속이 안되는 현성이 나타났다.
Cloudflare에서는 https로 접근할 경우 SSL인증을 자동으로 해줘서 되는거 였는데
근데 생각해보면 자동으로 해주면 안되는거 아닌가...
  
여튼, Route 53을 이용하더라도 https 접근이 가능해야하므로 방법을 찾아보니 ACM(AWS Certificate Manager)가 있다. SSL/TLS 인증서를 쉽게 프로비저닝, 관리, 배포할 수 있게 해준다고 한다.

[공식문서](http://docs.aws.amazon.com/ko_kr/acm/latest/userguide/acm-overview.html)

AWS CLI로도 할 수 있지만 그냥 콘솔에서 했다.
<br>

### 1. 인증서 요청

- 콘솔의 Servies중 Security, Identity & Compliance -> Certificate Manager가 있다.
- 인증서 요청을 클릭하면 SSL/TLS 인증서를 사용할 도메인을 입력할 수 있다.
- 검토 및 요청을 선택하여 다음 단계

<br>

### 2. 검토 및 요청

- 앞 단계에서 입력한 도메인의 소유자에게 인증서 신청 확인 이메일이 온다.
- 메일의 링크를 따라가 나오는 웹페이지에서 `I Approve`를 클릭하면 인증서가 발급되며 콘솔에서 확인 가능.
- 하지만 사용하고 있는 상태는 아니다.

<br>

### 3. 발급된 인증서 적용

- 발급된 SSL/TLS 인증서가 적용되어야 하는 곳은 처음 요청을 받게되는 Elastic Beanstlk이다.
- EB가 EC2를 이용하고 있는 것이므로, EC2 Dashboard의 Load Balancer의 Listeners에 HTTPS를 추가한다.
- 포트 443이 자동으로 지정되고, 아까 ACM에서 발급받은 SSL/TLS 발급받은 인증서를 선택할 수 있다.
- 외부에서 발급받은 인증서도 여기서 설정이 가능하다.
- EB의 Security Group의 Inbound에도 https를 추가하면 완료.
- ACM 콘솔로 돌아가 확인해보면 발급받았던 인증서가 사용중이라고 나온다.
- 웹 브라우저에서 https://pickycookbook.co.kr로 접근이 가능한 것을 확인


[참고](http://interconnection.tistory.com/21)


