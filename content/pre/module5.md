+++
title = "AWS WAF 로깅 활성화"
weight = 6
pre = "<b>1.5 </b>"
+++

* * *

AWS WAF는 Amazon Kinesis Firehose를 사용하여 로그를 저장합니다. 이를 통해 Amazon S3, Amazon Redshift 또는 Amazon Elastic Search와 같은 모든 Kinesis Firehose 대상으로 로그를 전달하고 또 분석할 수 있습니다. 웹 ACL에서 요청을 로깅하려면 먼저 Kinesis Data Firehose를 생성해야 하는데, 해당 실습에서는 이미 [모듈 1.](/pre.html) 에서 CloudFormation 스택을 통해 Kinesis Firehose와 최종 대상인 S3 bucket을 생성했습니다. 

이 실습의 로깅 활성화를 한 뒤 [모듈 5.](/logging.html)에서 로깅 내역을 확인해볼 예정입니다. 

- 우선 Kinesis Firehose가 잘 생성되었는지 확인해보겠습니다. [링크](https://ap-northeast-2.console.aws.amazon.com/kinesis/home?region=ap-northeast-2#/dashboard)를 클릭히여 kinesis 콘솔로 이동합니다. 

- 다음과 같이 'aws-waf-log-'로 시작하는 kinesis firehose delivery stream이 생성되어있는 것을 확인합니다. 
![DVWA Creation](/images/log1.png)


{{% notice info %}}
AWS WAF에서 kinesis로 로그를 스트리밍하기 위해서는 접두사 aws-waf-logs-로 시작하는 이름을 사용하여 Amazon Kinesis Data Firehose를 생성해야합니다. 
{{% /notice %}}

- 다시 WAF 콘솔로 돌아와 이번에는 로깅을 활성화 해보겠습니다. 

- WebACL "*MyWAF*" 에서 **Logging and Metrics** 탭으로 이동하여 Logging이 **Disable**되어있는 것을 확인하고 "Enable Logging"을 클릭합니다. 
![DVWA Creation](/images/log2.png)

- Amazon Kinesis Data Firehose Delivery Stream에서 CloudFormation으로 자동생성된 "aws-waf-logs-test"를 선택합니다. 
![DVWA Creation](/images/log3.png)

- 하기의 Redacted fields에서는 필요없다고 생각되는 필드인 "*Query string*"을 클릭합니다. 이 설정으로 인해 로그에는 Query string값이 기록되지 않습니다. 설정이 끝나면 "Enable logging"을 클릭하여 저장합니다. 
![DVWA Creation](/images/log4.png)

- 다음과 같이 Logging이 **Enable**된 것을 확인할 수 있습니다. 
![DVWA Creation](/images/log5.png)

- 이제 다음 모듈부터 진행할 공격 테스트 및 차단 테스트는 모두 kinesis firehose를 타고 S3 버킷에 쌓이게 됩니다. 