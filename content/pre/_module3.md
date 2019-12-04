+++
title = "Chrome Extention 설치"
weight = 4
pre = "<b>1.3 </b>"
+++

* * *
AWS WAF 에서는 국가별 공인 IP 를 기준으로 트래픽을 허용/차단 하는 기능을 제공하고 있습니다. 랩 과정에서 지정된 국가를 차단하는 환경을 가상으로 구성하기위하여 Chrome 에서 사용할 수 있는 "Browsec VPN" 을 설치하도록 하겠습니다.

[Chrome Store](https://chrome.google.com/webstore/search/browsec) 링크를 클릭한 후 아래와 같이 Browsec Extension 을 선택한 후 "Add to Chrome" 버튼을 클릭합니다.

![Lab Diagram](/images/chrome_extension.png)

아래와 같이 Extension 설치를 확인하는 확인창이 뜨면 "Add Extension" 을 클릭하여 설치를 계속합니다.

![Lab Diagram](/images/chrome_extension1.png)

설치된 Browsec VPN Exntension 은 이후 실습 과정에서 브라우저의 출발지 국가 정보를 변경하여 AWS WAF 의 국가별 차단 기능을 점검하는데 사용됩니다.

{{% notice info %}}
 Browsec VPN Extension 은 사용자의 필요에 따라 Chrome 에서 실습 이후에도 사용하실 수 있으며 불필요한 경우 Lab 종료 이후에 삭제하시기 바랍니다.
{{% /notice %}}