+++
title = "AWS WAF Web ACL 구성"
weight = 5
pre = "<b>1.4 </b>"
+++

* * *

이번에는 웹 공격을 방어하기 위한 AWS WAF 를 구성해보도록 하겠습니다.

AWS WAF 를 구성하는 방법은 여러가지가 있지만 본 실습에서는 Web ACL 을 먼저 생성한 후 
이후 [모듈 3.](/mitigation.html)과 [모듈 4.](/mitigation_deep.html) 에서 각 공격 유형별로 Rule 을 생성하여 Web ACL 에 추가하는 방법을 따르도록 하겠습니다.
  
  {{% notice info %}}
 현재 AWS WAF 는 기존에 제공되던 AWS WAF 메뉴와 함께 새로운 AWS WAF v2 메뉴가 제공되고 있습니다. 본 실습에서는 AWS WAF v2 를 기준으로 진행되기 때문에 반드시 새로운 AWS WAF 메뉴를 선택하신 후 진행하시기 바랍니다.
{{% /notice %}}


- AWS WAF 콘솔로 이동합니다. [링크](https://console.aws.amazon.com/wafv2/home?region=ap-northeast-2)를 클릭해서 이동할 수 있습니다. 

- 아래와 같이 AWS WAF 메뉴에서 Web ACL 을 선택한 후 "Create Web ACL" 버튼을 클릭합니다.
 ![DVWA Setting](/images/waf_create_acl0.png)  

- 먼저 화면 중간의 "Resource Type" 을 "Regional Resources" 로 선택한 후 "Region" 을 "Asia Pacific(Seoul)" 로 선택하시기 바랍니다. Region 선택이 끝나신 후 "Name" 에 적당한 이름을 입력하시기 바랍니다. "Name" 을 입력한 후 TAB 을 누르시면 "Cloudwatch Metric Name" 이 Web ACL Name 과 동일한 이름으로 자동입력 됩니다.
 ![DVWA Setting](/images/waf_create_acl1.png)

- 생성되는 WebACL 에 리소스를 할당하기 위하여 "Add AWS Resources" 버튼을 클릭합니다.
 ![DVWA Setting](/images/waf_create_acl2.png)
 
- "Add AWS Resources" 화면에서 이전 과정에서 생성되었던 ALB 를 선택한 후 "Add" 버튼을 클릭합니다.
 ![DVWA Setting](/images/waf_create_acl3.png)
 
- 아래와 같이 ALB 가 정상적으로 추가된 것을 확인한 후 "Next" 버튼을 클릭합니다.
 ![DVWA Setting](/images/waf_create_acl4.png)
 
- Rule 설정은 이후 과정에서 진행할 것이므로 그대로두고 화면 하단의 "Default Action" 이 "Allow" 로 되어 있는 것을 확인한 후 "Next" 버튼을 클릭합니다.
 ![DVWA Setting](/images/waf_create_acl5.png)
 
- 설정된 Rule 없으므로 "Set Rule Priority" 에서 "Next" 를 클릭합니다.
 ![DVWA Setting](/images/waf_create_acl6.png)
 
- "Configure Metrics" 에서도 "Next" 를 클릭합니다.
 ![DVWA Setting](/images/waf_create_acl7.png)
 
- 지금까지 설정한 내용이 모두 맞는지 확인한 후 "Create Web ACL" 버튼을 클릭합니다.
 ![DVWA Setting](/images/waf_create_acl8.png)
  
정상적으로 진행되었다면 아래 화면과 같이 새로운 Web ACL 이 생성되는 것을 확인할 수 있습니다.
 ![DVWA Setting](/images/waf_create_acl9.png)
 


 