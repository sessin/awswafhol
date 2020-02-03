+++
title = "실습 안내"
weight = 1
pre = "<b>1.1 </b>"
+++
* * *
AWS WAF는 일반적인 웹 취약점 공격으로부터 웹 애플리케이션을 보호하는 데 도움이 되는 웹 애플리케이션 방화벽입니다. AWS WAF를 사용하면 사용자 정의 가능한 웹 보안 규칙을 정의함으로써 어떤 트래픽에 웹 애플리케이션에 대한 엑세스를 허용하거나 차단할지 제어할 수 있습니다. AWS WAF는 SQL 명령어 주입이나 교차 사이트 스크립팅 등 공격 패턴을 차단하는 사용자 지정 규칙과 특정 애플리케이션을 위해 설계된 규칙을 생성할 수 있습니다. EC2 상에서 작동하는 웹 서버 앞의 ALB (Application Load Balancer)나 CDN 서비스인 CloudFront 중 하나에 AWS WAF를 배포할 수 있습니다.

이번 실습에서는 위협 요인이 내재된 인프라 환경 (로드밸런서-웹/데이터베이스 서버)을 구성하고, 몇 가지 취약점을 확인합니다.  이후 AWS WAF를 해당 시스템에 적용하고, SQL Injection, XSS (Cross Site Scripting) 등의 공격을 차단하는 실습을 진행합니다.
실습은 서울 리전(Seoul Region, ap-northeast-2)에서 진행되며, 약 90분 정도의 시간에 맞춰 구성되었고, AWS에 경험이 있으신 분들은 더 빠른 시간 내에 실습을 완료하실 수 있습니다. 

①	위협 요인이 내재된 인프라 환경을 구성하기 위해 CloudFormation 템플릿을 실행합니다. 템플릿 실행을 통해 생성되는 리소스는 VPC (Virtual Private Cloud), ALB (Application Load Balancer), EC2인스턴스 (Linux, Apache, MySQL, PHP) 등 입니다. 
②	AWS WAF가 적용되지 않은 환경에서 웹 취약점 (SQL Injection, XSS)을 확인합니다.

③	AWS WAF와 미리 설정된 WebACLs (Rules, Conditions)을 생성하기 위해 CloudFormation 템플릿을 실행합니다. 템플릿 실행을 통해서 WebACL 1개, Rules 9개, 그리고 다수의 Conditions이 생성됩니다.

④	AWS WAF의 ACLs이 생성된 후에는 WAF ACL과 ALB에 연결 (Association)합니다.

⑤	AWS WAF가 적용된 상태에서 1) SQL Injection, 2) XSS, 3) Bad bot 공격 차단 테스트를 수행합니다. 이후, Chrome Extention( User-Agent, VPN)을 설치하고, 4) Geo (지역) 5) String Maching 등의 차단 테스트를 수행합니다.

⑥	실습이 끝난 후 CloudFormation을 삭제합니다.

* * *
### 실습을 통해 생성되는 AWS 자원
| AWS 서비스 유형| 리소스명	| 기타 |
|-------------|--------|-----|
|EC2 인스턴스	 |WAFLab-WebServerInstance	| t2.micro|
|ALB|	MyDVW-Applica…|	-|
|VPC|	VPC|	10.10.0.0/16|
|VPC Subnet|	PublicSubnet	|10.10.0.0/18|
|VPC Subnet|	PrivateSubnet	|10.10.64.0/18|
|WAF WebACLs|	WAFRule	|-
|기타 서비스|	Elastic IP, Route table, Security Groups, Network ACL, IAM Role 등|


* * *

사전 준비 단계에서 사용되는 CloudFormation 에서는 아래와 같은 AWS 리소스를 생성하여 실습 환경을 구성합니다.
![Lab Diagram](/images/waflab_diagram.png)