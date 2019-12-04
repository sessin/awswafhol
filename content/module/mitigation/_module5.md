+++
title = "JSON 기반 Rule 설정"
weight = 5
pre = "<b>3.5 </b>"
+++

* * *
 이번에는 AWS WAF v2 에서 새롭게 제공되는 Rule 설정 방식인 JSON 기반 Rule 생성을 해보도록 하겠습니다. 빠른 실습 진행을 위하여 지금까지 생성하였던 Rule 들을 삭제하고 동일한 Rule 을 JSON 기반으로 생성하도록 하겠습니다.
 
 먼저, 현재까지 생성된 Rule 을 JSON 기반 문서로 다운로드하기 위하여 아래와 같이 Web ACL 의 화면 우측 상단의 "Download web ACL as JSON" 버튼을 클릭한 후 파일을 저장합니다.
 ![DVWA Setting](/images/jsonedit1.png)

- 저장된 파일은 여러분들이 지금까지 실습을 진행하면서 생성하였던 Rule 정보들을 포함하고 있으며 별다른 추가 설정을 하지 않았다면 아래와 같은 내용을 담고 있습니다.
 
```
{
  "Name": "MyWAF",
  "Id": "db5904b5-ccb4-4b6d-ac97-2711cb088072",
  "ARN": "arn:aws:wafv2:ap-northeast-2:852393119917:regional/webacl/MyWAF/db5904b5-ccb4-4b6d-ac97-2711cb088072",
  "DefaultAction": {
    "Allow": {}
  },
  "Description": "",
  "Rules": [
    {
      "Name": "SG-Block",
      "Priority": 0,
      "Statement": {
        "GeoMatchStatement": {
          "CountryCodes": [
            "SG"
          ]
        }
      },
      "Action": {
        "Block": {}
      },
      "VisibilityConfig": {
        "SampledRequestsEnabled": true,
        "CloudWatchMetricsEnabled": true,
        "MetricName": "SG-Block"
      }
    },
    {
      "Name": "XSS-Rule",
      "Priority": 1,
      "Statement": {
        "XssMatchStatement": {
          "FieldToMatch": {
            "AllQueryArguments": {}
          },
          "TextTransformations": [
            {
              "Priority": 0,
              "Type": "URL_DECODE"
            }
          ]
        }
      },
      "Action": {
        "Block": {}
      },
      "VisibilityConfig": {
        "SampledRequestsEnabled": true,
        "CloudWatchMetricsEnabled": true,
        "MetricName": "XSS-Rule"
      }
    },
    {
      "Name": "SQL-Ruie",
      "Priority": 2,
      "Statement": {
        "SqliMatchStatement": {
          "FieldToMatch": {
            "AllQueryArguments": {}
          },
          "TextTransformations": [
            {
              "Priority": 0,
              "Type": "URL_DECODE"
            }
          ]
        }
      },
      "Action": {
        "Block": {}
      },
      "VisibilityConfig": {
        "SampledRequestsEnabled": true,
        "CloudWatchMetricsEnabled": true,
        "MetricName": "SQL-Ruie"
      }
    }
  ],
  "VisibilityConfig": {
    "SampledRequestsEnabled": true,
    "CloudWatchMetricsEnabled": true,
    "MetricName": "MyWAF"
  },
  "Capacity": 81
}
```

- Rule 설정을 백업하였으니 이번에는 Web ACL 에서 사용하고 있는 Rule 들을 모두 삭제하도록 하겠습니다. Web ACL 의 Rules 탭으로 이동한 후 아래와 같이 현재 설정되어 있는 Rule 을 모두 선택한 후 "Delete" 버튼을 클릭합니다.
 ![DVWA Setting](/images/jsonedit2.png) 

- 아래와 같이 Rule 삭제를 위하여 확인창이 나타나면 "delete" 를 입력해주고 "Delete" 버튼을 클릭하여 Rule 을 삭제합니다.
 ![DVWA Setting](/images/jsonedit3.png)
 
- 아래와 같이 모든 Rule 이 삭제된 상태에서 지금까지 사용했던 공격 방법 및 Singapore 에서의 접속 등이 모두 차단되지 않고 정상적으로 접속되는지 확인합니다.
 ![DVWA Setting](/images/jsonedit4.png)

***
- 이제 JSON 기반 Rule 설정을 해보도록 하겠습니다. 아래와 같이 새로운 Rule 을 추가하기 위하여 "Add my own rules and rule gruops" 버튼을 클릭합니다.
 ![DVWA Setting](/images/rulegroup_2.png) 

- JSON 기반의 Rule 설정을 하기 위해서 Rule Builder 를 아래 화면과 같이 "Rule JSON editor" 를 선택합니다.
 ![DVWA Setting](/images/jsonedit5.png)
 
- JSON 구문을 넣는 곳에 아래의 Rule 을 복사하여 붙여넣기 한 후 "Validate" 버튼을 클릭하여 문법에 이상이 없는지 확인합니다. "Rule is valid" 라는 문구를 확인하였다면 화면 하단의 "Add Rule" 버튼을 클릭하여 JSON 기반의 Rule 을 추가합니다.
``` 
 {
  "Name": "SG-Block",
  "Priority": 0,
  "Statement": {
    "GeoMatchStatement": {
      "CountryCodes": [
        "SG"
      ]
    }
  },
  "Action": {
    "Block": {}
  },
  "VisibilityConfig": {
    "SampledRequestsEnabled": true,
    "CloudWatchMetricsEnabled": true,
    "MetricName": "SG-Block"
  }
}
```
- 첫번째 Rule 생성에 성공하였다면 2번쨰로 아래의 JSON Rule 을 이용하여 XSS-Rule 을 생성합니다.
 ```
{
  "Name": "XSS-Rule",
  "Priority": 1,
  "Statement": {
    "XssMatchStatement": {
      "FieldToMatch": {
        "AllQueryArguments": {}
      },
      "TextTransformations": [
        {
          "Priority": 0,
          "Type": "URL_DECODE"
        }
      ]
    }
  },
  "Action": {
    "Block": {}
  },
  "VisibilityConfig": {
    "SampledRequestsEnabled": true,
    "CloudWatchMetricsEnabled": true,
    "MetricName": "XSS-Rule"
  }
}
```
- 마지막으로 아래의 JSON Rule 을 이용하여 XSS-Rule 을 생성합니다.
```
{
  "Name": "SQL-Ruie",
  "Priority": 2,
  "Statement": {
    "SqliMatchStatement": {
      "FieldToMatch": {
        "AllQueryArguments": {}
      },
      "TextTransformations": [
        {
          "Priority": 0,
          "Type": "URL_DECODE"
        }
      ]
    }
  },
  "Action": {
    "Block": {}
  },
  "VisibilityConfig": {
    "SampledRequestsEnabled": true,
    "CloudWatchMetricsEnabled": true,
    "MetricName": "SQL-Ruie"
  }
}
```

- 아래와 같이 모든 Rule 의 생성이 완료되었다면 이전 실습과정에서 진행하였던 SQL Injection 공격, XSS 공격, Singapore 에서의 IP 등이 모두 정상적으로 차단되는지 확인합니다.
 ![DVWA Setting](/images/jsonedit7.png)
