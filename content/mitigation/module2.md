+++
title = "custom rule 추가 1"
weight = 2
pre = "<b>3.2 </b>"
+++

* * *
 이번에는 공격 타입 별 Custom Rule을 작성하여 적용해보록 하겠습니다. 
 
 첫번째로 AWS WAF 에서 제공하는 국가별 IP 정보를 기준으로 특정 국가에서 유입되는 트래픽을 차단하는 실습을 진행하도록 하겠습니다. 
 

### Chrome Extension 설정 

차단 설정을 하기에 앞서 사용자의 PC 에서 발생하는 트래픽이 특정 국가에서 발생되는 것처럼 환경을 설정하기 위하여 이전 단계에서 설치하였던 Chrome Extension 을 사용하도록 하겠습니다.

- 크롬 브라우저에서 Browsec VPN 을 선택한 후 아래와 같이 "OFF" 를 "On" 으로 변경한 후 "Change" 버튼을 클릭하여 사용하고자하는 국가를 선택합니다.

 ![DVWA Setting](/images/browsec1.png)

 {{% notice info %}}
 Browsec 메뉴에서 Premium 으로 표기되어 있는 국가는 별도의 과금이 발생하는 국가이니 실습 과정에서는 반드시 무료 국가를 선택하시기 바랍니다.
 {{% /notice %}}

- 본 실습에서는 Singapore 를 선택하도록 하겠습니다.
 ![DVWA Setting](/images/browsec2.png)

- 이제 Browsec 이 "On" 되어 있는 상태에서는 브라우저에서 발생하는 모든 트래픽은 Singapore 에서 발생되는 것처럼 트래픽이 전송되게 됩니다. 이 상태에서 DVWA 페이지가 정상적으로 접속이 되는지 확인합니다.

### Rule 추가

- 페이지가 정상적으로 접속이 된다면 이번에는 Singapore 에서 유입되는 트래픽을 차단하는 Rule을 Web ACL 에 추가하도록 하겠습니다. Web ACL 에 새로운 Rule 을 추가하기 위하여 아래와 같이 선택한 Web ACL 의 상세 화면 중 상단의 "Rules" 를 선택한 후 화면 우측의 "Add rules" 메뉴를 클릭합니다. 이 메뉴를 클릭하면 하위 메뉴를 확인할 수 있는데 하위 메뉴 중 "Add my own rules and rule groups" 메뉴를 클릭합니다. 이 메뉴를 선택하면 새로운 WAF Rule 을 생성하거나 미리 만들어 둔 Rule Group 을 Web ACL 에 추가할 수 있습니다.

 ![DVWA Setting](/images/country_block1.png)
 
- 새로운 Rule 을 생성하기 위하여 다음과 같이 여러 옵션들을 정의합니다. 아래 3가지를 제외한 나머지는 모두 기본값으로 선택합니다.
  1. Name = 임의의 이름 입력 (ex. SG-Block)
  2. Inspect = Originates from a country in 선택
  3. Country Codes = Singapore - SG 선택
 ![DVWA Setting](/images/country_block2.png)
 
- 생성하려고하는 Rule 의 Default Action 이 Block 인 것을 확인한 후 "Add Rule" 버튼을 클릭합니다.
 ![DVWA Setting](/images/rulegroup_4.png)

- 정상적으로 진행되는 경우 아래와 같이 새로운 Rule 생성이 되고 "Set rule priority" 화면으로 진행이 되게 되는데 별도의 Priority 설정이 필요 없으므로 "Save" 버튼을 클릭합니다.
 ![DVWA Setting](/images/country_block3.png)

- Web ACLs 화면에서 "Rules" 탭을 클릭하여 새로운 Rule 이 생성된 것을 확인합니다. 아래 화면과 같이 생성된 Rule 이 901 WCU 을 점유하는 것을 확인합니다.
 ![DVWA Setting](/images/country_block4.png)
 
### 적용한 Rule 테스트

- 이제 Singapore 에서 발생하는 트래픽을 차단할 수 있는 Rule 이 Web ACL 에 추가되었으므로 크롬 브라우저에서 다시 한 번 DVWA 로 접속해보도록 하겠습니다.
 
- 모든 설정이 정상적으로 이뤄졌다면 아래와 같이 "403 Forbidden" 메시지와 함께 차단된 것을 확인할 수 있습니다.
 ![DVWA Setting](/images/blocked.png)

- 국가별 차단 기능을 확인하였으므로 Browsec 을 아래와 같이 "Off" 하도록 합니다.
 ![DVWA Setting](/images/country_block5.png) 