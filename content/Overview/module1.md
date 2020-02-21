+++
title = "사전 지식"
weight = 1
pre = "<b>0-1. </b>"

+++

## **AWS WAF**

AWS WAF는 Amazon CloudFront 배포, Amazon API Gateway API 또는 Application Load Balancer에 전달되는 HTTP(S) 요청을 모니터링할 수 있게 해주는 웹 애플리케이션 방화벽입니다.

또한 AWS WAF을 사용하여 콘텐츠에 대한 액세스를 제어할 수 있습니다. 요청이 허용되는 IP 주소나 쿼리 문자열의 값으로부터 지정하는 조건 등 지정하는 조건에 따라, Amazon CloudFront 배포, Amazon API Gateway API 또는 Application Load Balancer는 요청된 콘텐츠나 HTTP 403 상태 코드(금지됨)로 요청에 응답합니다. 또한 요청이 차단될 때 사용자 지정 오류 페이지를 반환하도록 CloudFront를 구성할 수 있습니다.

본 실습에서는 웹 공격에 취약하도록 의도된 web application 을 Application Load Balancer에 연결하고, AWS WAF를 통해 공격에 방어하는 체계를 구성할 예정입니다. 

{{% notice tip %}}
 AWS WAF에 대한 더 자세한 사항은 [AWS Document](https://docs.aws.amazon.com/ko_kr/waf/latest/developerguide/waf-chapter.html) 를 참고해주시기 바랍니다. 
{{% /notice %}}



## **AWS CloudFormation**

AWS CloudFormation은 Amazon Web Services 리소스를 모델링하고 설정하여 리소스 관리 시간을 줄이고 AWS에서 실행되는 애플리케이션에 더 많은 시간을 사용하도록 해 주는 서비스입니다. 필요한 모든 AWS 리소스(예: Amazon EC2 인스턴스 또는 Amazon RDS DB 인스턴스)를 설명하는 템플릿을 생성하면 AWS CloudFormation이 해당 리소스의 프로비저닝과 구성을 담당합니다. AWS 리소스를 개별적으로 생성하고 구성할 필요가 없으며 어떤 것이 무엇에 의존하는지 파악할 필요도 없습니다. AWS CloudFormation에서 모든 것을 처리합니다. 다음 시나리오는 AWS CloudFormation이 얼마나 유용한지를 보여줍니다.

본 실습에서는 웹 공격에 취약하도록 의도된 web application 환경을 구성하기 위해 CloudFormation 템플릿을 실행합니다. 

{{% notice tip %}}
 AWS CloudFormation에 대한 더 자세한 사항은 [AWS Document](https://docs.aws.amazon.com/ko_kr/AWSCloudFormation/latest/UserGuide/Welcome.html) 를 참고해주시기 바랍니다. 
{{% /notice %}}


