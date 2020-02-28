+++
title = "AWS Managed Rule 추가"
weight = 1
pre = "<b>3.1 </b>"
+++

* * *

 Web ACL 에 Rule 을 적용하기 위해서는 Rule 이나 Rule Group 을  생성하여야 합니다. 관리자는 적용하고자 하는 목적에 따라 AWS 가 관리하는 AWS Managed Rule 을 사용하거나 3rd Party 파트너가 제공하는 관리형 Rule Group 을 사용할 수도 있습니다. 아니면 Managed Rule 이나 Rule Group 을 사용하지 않고 공격 타입별로 각각의 Rule 을 생성한 후 Web ACL 에 적용할 수도 있습니다. 

 여기서는 AWS Managed Rule을 적용해보도록 하겠습니다. 

### AWS Managed Rule을 적용 

- 실습에 사용할 새로운 Rule 을 Web ACL 에 추가하기 위하여 좌측의 AWS WAF 메뉴에서 Web ACL 을 선택합니다. 리전이 **"Asia Pacific(Seoul)"** 로 선택되어 있는 것을 확인한 후 하단의 Web ACL 리스트 중 이전 과정에서 생성한 Web ACL 을 클릭합니다.
 
 {{% notice info %}}
 Web ACL 메뉴를 클릭하면 선택되어 있는 리전이 Seoul Region 이 아닐 수도 있으므로 반드시 확인하시기 바랍니다.
 {{% /notice %}}

 ![DVWA Setting](/images/rulegroup_1.png)
 
- 선택한 Web ACL 의 상세 화면 중 상단의 "Rules" 를 선택한 후 화면 우측의 "Add rules" 메뉴를 클릭합니다. 이 메뉴를 클릭하면 하위 메뉴를 확인할 수 있는데 하위 메뉴 중 "Add managed rule groups" 메뉴를 클릭합니다. 이 메뉴를 선택하면 AWS Managed Rule 혹은 3rd Party 파트너가 제공하는 관리형 Rule Group 을 Web ACL 에 추가할 수 있습니다.

 ![DVWA Setting](/images/rulegroups_2.png) 

- 가장 상단의 **AWS managed rule groups** 를 클릭하면 적용가능한 rule group들이 나타납니다. 
- 이중에서 **Core rule set** 과 **SQL database** 에 대해 "Add to web ACL"을 클릭하고 하단의 "Add rules"를 클릭합니다.  

 ![DVWA Setting](/images/rulegroups_3.png) 

 {{% notice info %}}
 **Core rule set** rule group 에는 일반적으로 웹 애플리케이션에 적용할 수 있는 Rule이 포함되어 있습니다. 이러한 규칙은 OWASP 발행물 및 수많은 CVE(일반적인 취약성 및 노출도)에 설명된 취약성을 포함하여 광범위한 취약성을 악용하는 일이 없도록 보호합니자세한 사항은 [AWS DOCS](https://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups-list.html)를 참고해주시기 바랍니다. 
 {{% /notice %}}

 {{% notice info %}}
 **SQL database** rule group 에는 SQL 주입 공격과 같은 SQL 데이터베이스 악용과 관련된 요청 패턴을 차단하는 Rule이 포함되어 있습니다. 이렇게 하면 승인되지 않은 쿼리가 원격으로 삽입되는 것을 방지할 수 있습니다. 자세한 사항은 [AWS DOCS](https://docs.aws.amazon.com/waf/latest/developerguide/aws-managed-rule-groups-list.html)를 참고해주시기 바랍니다. 
 {{% /notice %}}

**Set rule priority**에서는 기본값을 그대로 두고 "save" 버튼을 클릭하여 내용을 저장합니다. 
다음과 같이 정상적으로 추가된 것을 확인할 수 있습니다. 

 ![DVWA Setting](/images/rulegroups_4.png) 
 

### 적용한 Rule 테스트 

적용한 Rule들이 정상적으로 동작을 하는지 확인하기 위해 앞서 모듈 1에서 구성했던 DVWA 웹에 접속해서 모듈 2에서 실행했던 **SQL injection** 과 **XSS exploit**를 재시도 해봅니다. 
 
- 모든 설정이 정상적으로 이뤄졌다면 아래와 같이 이전 과정에서 차단되지 않았던 **SQL injection** 구문이 "403 Forbidden" 메시지와 함께 차단된 것을 확인할 수 있습니다.

  ```
  ' OR 1=1 #  
  ```
  
 ![DVWA Setting](/images/DVWA_sqlinjection1.png)

 ![DVWA Setting](/images/blocked.png)

- 모든 설정이 정상적으로 이뤄졌다면 아래와 같이 이전 과정에서 차단되지 않았던 **XSS exploit** 구문 역시 "403 Forbidden" 메시지와 함께 차단된 것을 확인할 수 있습니다.

  ```
  <script>alert(document.cookie)</script>
  ```
  
 ![DVWA Setting](/images/DVWA_xss1.png)

 ![DVWA Setting](/images/blocked.png)