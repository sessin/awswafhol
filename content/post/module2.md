+++
title = "AWS 자원 삭제"
weight = 2
pre = "<b>6.2 </b>"
+++
* * *

 본 실습 과정에서 사용된 AWS 자원은 크게 2가지 유형으로 생성되었습니다. 하나는 CloudFormation 을 통하여 자동으로 생성되었고 하나는 Web ACL 로 여러분들이 각각 수작업으로 생성이 되었습니다. 따라서, 실습에 사용된 AWS 자원을 삭제하려면 사용된 CloudFormation 을 삭제하고 Web ACL 을 삭제하셔야 합니다.
***
## 1. Web ACL 삭제
 Web ACL 을 삭제하기 위해서는 먼저 Web ACL 과 연결되어 있는 AWS Resource 를 제거하여야 합니다. 실습 과정에서 ALB 와의 연결을 설정하였으므로 ALB 와의 연결을 삭제하도록 하겠습니다.
 ALB 연결을 제거하기 위하여 Web ACL 메뉴의 "Associated AWS resources" 를 클릭한 후 실습에 사용된 ALB 를 선택합니다. 선택된 ALB 를 삭제하기 위하여 "Remove" 버튼을 클릭합니다.
![XSS Exploit](/images/delete3.png)
아래와 같이 경고창이 나타나면 "delete" 를 입력한 후 "Delete" 버튼을 클릭합니다.
![XSS Exploit](/images/delete5.png)
이제 Web ACL 과 연결되어 있는 ALB 를 삭제하였으므로 Web ACL 을 삭제할 수 있습니다. Web ACL 을 삭제하기 위하여 Web ACL 의 기본 메뉴에서 아래와 같이 실습에 사용된 Web ACL 을 선택한 후 "Delete" 버튼을 클릭합니다.
![XSS Exploit](/images/delete2.png)
아래와 같이 경고창이 나타나면 "delete" 를 입력한 후 "Delete" 버튼을 클릭합니다.
![XSS Exploit](/images/delete4.png)
모든 과정을 정상적으로 진행하였다면 아래와 같이 Web ACL 이 삭제된 것을 확인할 수 있습니다.
![XSS Exploit](/images/delete6.png)
***

## 2. S3 bucket 삭제

[S3 관리 콘솔](https://console.aws.amazon.com/s3/home?region=ap-northeast-2)에 접속한 후 로그 적재에 사용되었던 S3 bucket 을 삭제합니다. 


## 2. CloudFormation 삭제

[CloudFormation 관리 콘솔](https://ap-northeast-1.console.aws.amazon.com/cloudformation/home?region=ap-northeast-2)에 접속한 후 DVWA 생성에 사용되었던 CloudFormation 을 삭제합니다. 

아래와 같이 실습에 사용된 CloudFormation 을 선택한 후 "삭제" 버튼을 클릭합니다. 
![XSS Exploit](/images/delete1.png)
삭제를 확인하는 경고창이 나타나면 "스택 삭제" 버튼을 클릭합니다.
![XSS Exploit](/images/delete7.png)

 {{% notice info %}}
CloudFormation 삭제에는 시간이 소요됩니다. 몇 분이 흐른 후 CloudFormation 이 정상적으로 삭제되었음을 확인하시기 바랍니다.
{{% /notice %}}
***


### 이제 모든 실습 과정이 종료되었습니다. 수고하셨습니다!!