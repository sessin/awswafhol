+++
title = "XSS 공격 차단"
weight = 3
pre = "<b>3.3 </b>"
+++

* * *
 이번에는 XSS 공격을 차단할 수 있는 Rule 을 생성하여 Web ACL 에 추가하도록 하겠습니다.
 
 - 실습에 사용할 새로운 Rule 을 Web ACL 에 추가하기 위하여 좌측의 AWS WAF 메뉴에서 Web ACL 을 선택합니다. 리전이 "Asia Pacific(Seoul)" 로 선택되어 있는 것을 확인한 후 하단의 Web ACL 리스트 중 이전 과정에서 생성한 Web ACL 을 클릭합니다.
 
 {{% notice info %}}
 Web ACL 메뉴를 클릭하면 선택되어 있는 리전이 Seoul Region 이 아닐 수도 있으므로 반드시 확인하시기 바랍니다.
 {{% /notice %}}

 ![DVWA Setting](/images/rulegroup_1.png)
 
- 선택한 Web ACL 의 상세 화면 중 상단의 "Rules" 를 선택한 후 화면 우측의 "Add rules" 메뉴를 클릭합니다. 이 메뉴를 클릭하면 하위 메뉴를 확인할 수 있는데 하위 메뉴 중 "Add my own rules and rule groups" 메뉴를 클릭합니다. 이 메뉴를 선택하면 새로운 WAF Rule 을 생성하거나 미리 만들어 둔 Rule Group 을 Web ACL 에 추가할 수 있습니다.
 ![DVWA Setting](/images/xssrule1.png)
 
- 새로운 Rule 을 생성하기 위하여 다음과 같이 여러 옵션들을 정의합니다. 아래 4가지를 제외한 나머지는 모두 기본값으로 선택합니다.
  1. Name = 임의의 이름 입력
  2. Inspect = All query parameters 선택
  3. Match Type = Contains XSS Injection Attacks 선택
  4. Text Transformation = URL decode 선택
 ![DVWA Setting](/images/xssrule2.png)
 
- 생성하려고하는 Rule 의 Default Action 이 Block 인 것을 확인한 후 "Add Rule" 버튼을 클릭합니다.
 ![DVWA Setting](/images/rulegroup_4.png)

- 정상적으로 진행되는 경우 아래와 같이 새로운 Rule 생성이 되고 "Set rule priority" 화면으로 진행이 되게 되는데 별도의 Priority 설정이 필요 없으므로 "Save" 버튼을 클릭합니다.
 ![DVWA Setting](/images/xssrule3.png)

- Web ACLs 화면에서 "Rules" 탭을 클릭하여 새로운 Rule 이 생성된 것을 확인합니다. 아래 화면과 같이 생성된 Rule 이 80 WCU 을 점유하는 것을 확인합니다.
 ![DVWA Setting](/images/xssrule4.png)
 
- 이제 SQL 공격을 차단할 수 있는 Rule 이 Web ACL 에 추가되었으므로 이전 과정에서 실행했던 XSS Injection 공격을 DVWA 화면에서 실행해보도록 하겠습니다.
- ALB DNS 주소를 통해 DVWA 화면에 접속한 후 이전 과정과 동일하게 XSS Injection(Reflected) 메뉴에서 아래의 XSS Injection 구문을 입력한 후 "Submit" 버튼을 클릭합니다.

```
<script>alert(document.cookie)</script>
```
  
 ![DVWA Setting](/images/DVWA_xss1.png)
 
- 모든 설정이 정상적으로 이뤄졌다면 아래와 같이 이전 과정에서 차단되지 않았던 XSS Injection 구문이 "403 Forbidden" 메시지와 함께 차단된 것을 확인할 수 있습니다.
 ![DVWA Setting](/images/blocked.png)
