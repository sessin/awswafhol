+++
title = "WAF 로깅"
weight = 1
pre = "<b>5.1 </b>"
+++


### AWS WAF 로깅 활성화 

AWS WAF는 Amazon Kinesis Firehose를 사용하여 로그를 저장합니다. 이를 통해 Amazon S3, Amazon Redshift 또는 Amazon Elastic Search와 같은 모든 Kinesis Firehose 대상으로 로그를 전달하고 또 분석할 수 있습니다. 웹 ACL에서 요청을 로깅하려면 먼저 Kinesis Data Firehose를 생성해야 하는데, 해당 실습에서는 이미 모듈 1 에서 CloudFormation 스택을 통해 Kinesis Firehose와 최종 대상인 S3 bucket을 생성했습니다. 

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

- 하기의 Redated fields에서는 필요없다고 생각되는 필드인 "*Query string*"을 클릭합니다. 이 설정으로 인해 로그에는 Query string값이 기록되지 않습니다. 설정이 끝나면 "Enable logging"을 클릭하여 저장합니다. 
![DVWA Creation](/images/log4.png)

- 다음과 같이 Logging이 **Enable**된 것을 확인할 수 있습니다. 
![DVWA Creation](/images/log5.png)




### WAF 로그 발생 

- 로그를 확인하기 위해 로그 발생을 시켜야합니다. 이전 모듈들에서 수행했던 공격이나 정상 요청을 몇가지 테스트 해본 뒤 잠시 기다립니다.

- S3 [콘솔](https://console.aws.amazon.com/s3/home?region=ap-northeast-2)로 이동한 뒤 "*mydvwa-*"로 시작하는 버킷을 찾은 뒤 가장 하위 경로로 내려가면 다음과 같이 로그가 쌓이는 것을 확인할 수 있습니다. 

![DVWA Creation](/images/log6.png)

- 생성된 파일 중 하나를 다운로드 하여 가장 익숙한 editor로 실행하고 살펴봅니다. 


### AWS WAF 로그 확인 

다음은 요청의 WAF 로그 예입니다. 요청 평가를 종료 한 규칙에 대한 세부 정보를 받습니다. 로그에는 해당 요청에 대한 조치도 포함됩니다.

![DVWA Creation](/images/log7.png)

- 해당 요청이 **TestRule**에 의해 차단이 되었는지에 대한 내용 및 관련 자세한 사항을 확인 할 수 있습니다. 
- 이전에 Redated fields 에서 선택했던 "*Query string*" 에 대한 필드인 args가 "*REDATED*" 로 표현되어있는 것을 확인 할 수 있습니다. 

- 이를 발전시켜 다양한 분석에 활용할 수 있습니다. 