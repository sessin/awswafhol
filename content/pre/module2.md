+++
title = "DVWA 확인"
weight = 3
pre = "<b>1.2 </b>"
+++

### DVWA 웹 페이지 접속 확인
DVWA 스택이 정상적으로 생성되었다면 템플릿을 통하여 생성된 DVWA 웹페이지에 정상적으로 접속이 되는지 확인해보도록 하겠습니다.

- AWS Management Console 의 EC2 메뉴하단에 새로운 ALB (Application Load Balancer)가 생성된 것을 확인한 후 해당 ALB 의 DNS 이름을 이용하여 인터넷 브라우져에서 접속합니다.
![DVWA Access](/images/DVWA_Access.png)

- 아래와 같이 DVWA 의 로그인 페이지로 접속이 가능한 것을 확인합니다.
![DVWA Login](/images/DVWA_login.png)

- *"ID = admin", "Password = password"* 를 입력하고 다음과 같이 DVWA 에 정상적으로 로그인이 되는 것을 확인합니다.
![DVWA Login](/images/DVWA_mainpage.png)


### DVWA 환경 설정

  본 실습에서 생성된 DVWA 서버는 기본적으로 주요 취약점을 사용할 수 없는 환경으로 설정이 되어 있습니다. 따라서, 실습 진행과정에서 공격을 쉽게 수행하기 위해서는 DVWA 의 Security Level 설정을 변경해주어야 합니다. 
  
- DVWA 에 접속한 후 다음과 같이 화면 하단의 "DVWA Security" 메뉴를 클릭합니다.
 
![DVWA Setting](/images/DVWA_setting1.png)
 
- DVWA Security 화면으로 이동한 후 화면 중간의 Pull Down 메뉴에서  기본값으로 설정되어 있는 "Impossible" 을 "Low" 로 변경한 후 "Submit" 버튼을 클릭합니다.
  
![DVWA Setting](/images/DVWA_setting2.png)
 