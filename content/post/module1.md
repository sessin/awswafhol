+++
title = "과정 복습"
weight = 1
pre = "<b>6.1 </b>"
+++

* * *


### 마치기 전에 복습

오늘 진행한 실습은 다음과 같은 절차로 이루어졌습니다. 

1. 위협 요인이 내재된 인프라 환경을 구성하기 위해 CloudFormation 템플릿을 실행했습니다. 템플릿 실행을 통해 생성되는 리소스는 VPC (Virtual Private Cloud), ALB (Application Load Balancer), EC2인스턴스 (Linux, Apache, MySQL, PHP), Kinesis Firehose, S3 bucket 등 입니다. 

2. AWS WAF가 적용되지 않은 환경에서 웹 취약점 (SQL Injection, XSS)을 확인했습니다. 

3. AWS Managed Rule과 custom Rule을 이용하여 다양한 Rule들을 작성하고 적용해 보았습니다. 

4. AWS WAF가 적용된 상태에서 1) SQL Injection, 2) XSS, 3) Bad bot 공격 차단 테스트를 수행해보고 정상적으로 차단이 되는 것으로 확인했습니다. 

5. AWS WAF 로그를 보고 어떤 내역들이 로깅되는지 확인해보았습니다. 

6. 실습이 끝난 후 CloudFormation을 삭제할 예정입니다. 

