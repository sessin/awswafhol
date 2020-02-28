+++
title = "실습 개요"
chapter = true
weight = 1
pre = "<b>0. </b>"

+++

***
본 실습에서는 웹 공격에 취약하도록 의도된 web application ( [DVWA](http://www.dvwa.co.uk/) ) 에서 AWS WAF 를 통해 웹 공격을 차단하는 방법에 대해 익혀봅니다.
실습은 약 1시간에서 1시간 반 정도 소요되며 크게 5개의 모듈로 진행됩니다.
***

##### [모듈 1.](/pre.html) **실습 환경구성** : 웹 공격에 취약한 web application 을 AWS CloudFormation 을 통해 구축합니다. 
##### [모듈 2.](/attack.html) **공격 테스트** : 잘 알려진 웹 공격 (SQLi , XSS expolit)으로 web application 을 공격해 봅니다. 
##### [모듈 3.](/mitigation.html) **AWS WAF를 이용한 방어** : AWS WAF의 AWS managed Rule 을 통해 기본적인 룰셋을 적용해보고 잘 방어가 되는지 테스트 해봅니다. 
##### [모듈 4.](/mitigation_deep.html) **AWS WAF를 이용한 방어(심화)** : AWS WAF의 custom Rule 을 통해 조금 더 복잡한 룰셋을 적용해보고 잘 방어가 되는지 테스트 해봅니다. 
##### [모듈 5.](/logging.html) **AWS WAF 로깅** : AWS WAF 로그를 로깅하고 확인해 봅니다. 
##### [모듈 6.](/post.html) **실습 구성 요소 삭제** : 생성했던 환경 자원들을 삭제합니다. 


{{% button href="mailto:yijeong@amazon.com" icon="fas fa-bug" %}}Report an issue{{% /button %}}
{{% button href="http://security.aws-korea.com" icon="fas fa-graduation-cap" %}}Learn more{{% /button %}}