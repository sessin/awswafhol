+++
title = "JSON 기반 Rule 설정"
weight = 2
pre = "<b>4.2 </b>"
+++

* * *
 
### Attack !! 

이번 실습에서는 가상의 상황을 가정해보도록 하겠습니다. 

당신은 팀의 보안 담당자 입니다. 서비스 하고 있는 웹 어플리케이션에서 최근에 한국IP로 지속적으로 공격이 들어오고 있어 확인을 해보니 다음과 같은 특징이 있었습니다.
1. 공격의 대부분은 한국에서 온 공격이다. 하지만 한국에서는 실제 고객들이 요청하는 정상 트래픽도 있다.
2. 한국에서 오는 공격은 **request body** 가 비정상적으로 커서 **100byte** 이상이거나 header "*x-value*" 의 값이 "*bot*"이나 "*BOT*"으로 들어온다.  

이제 당신은 새로운 규칙을 작성해서 정상 요청을 막지 않는 선에서 악의적인 공격을 막아야 합니다. 


### JSON 기반 Rule 작성 

{{% notice info %}}
중첩문 (nested statement)를 포함하는 Rule은 Rule visual editor에서 편집할 수 없습니다. 따라서 해당 시나리오에서는 JSON editor를 사용해서 Rule을 작성해야합니다. 
{{% /notice %}}

- 이제 JSON 기반 Rule 설정을 해보도록 하겠습니다. 아래와 같이 새로운 Rule 을 추가하기 위하여 "Add my own rules and rule gruops" 버튼을 클릭합니다.
 ![DVWA Setting](/images/rulegroup_2.png) 

- Rule Builder 에서 **Rule JSON editor**를 클릭합니다. 
 ![DVWA Setting](/images/json1.png) 

- 우선 JSON 문서에 Rule name 과 MetricName을 추가합니다. 둘다 "**TESTRule**"로 지정하겠습니다

```
{
  "Name": "TestRule",
  "Priority": 0,
  "Action": {
    "Block": {}
  },
  "VisibilityConfig": {
    "SampledRequestsEnabled": true,
    "CloudWatchMetricsEnabled": true,
    "MetricName": "TestRule"
  },
  "Statement": {}
}
```

- 위와 같은 요구사항을 맞추기 위해서는 중첩 구조가 필요합니다. 다음과 같은 구조로 작성할 수 있습니다.  

```
{
  "Name": "TestRule",
  "Priority": 0,
  "Action": {
    "Block": {}
  },
  "VisibilityConfig": {
    "SampledRequestsEnabled": true,
    "CloudWatchMetricsEnabled": true,
    "MetricName": "TestRule"
  },
  "Statements": {
    "AndStatement": {
      "Statements": [
        {
          //한국에서 들어오는 요청 조건 
        },
        {
          "OrStatement": {
            "Statements": [
              {
                //Request Body 크기에 대한 조건 
              },
              {
                //요청 헤더에 대한 조건 
              }
            ]
          }
        }
      ]
    }
  }
}
```

- JSON 구조에서 다음과 같이 AND 문안에 OR문이 중첩되어 있는 것을 확인할 수 있습니다. 
 ![DVWA Setting](/images/json2.png) 

- 힌트를 드릴테니 Rule을 완성해보시기 바랍니다. 

1. **국가기반 일치 조건**은 "*GeoMatchStatement*" 입니다. 
2. 한국의 "*CountryCodes*"는 "*KR*"입니다.
3. **크기제약 조건**은 "*SizeConstraintStatement*" 입니다. 
4. **비교연산자** "*ComparisonOperator*" 는 "*GT*"입니다. 
5. **문자열일치 조건**은 "*ByteMatchStatement*" 입니다. 
6. "*bot*"이나 "*BOT*" 을 모두 걸러낼 수 있는 **TextTransformations**는 "*LowerCase*" 입니다. 


{{%expand "정답 보기" %}}

- 완성된 Rule은 다음과 같은 모습을 보입니다. 

```

{
  "Name": "TestRule",
  "Priority": 0,
  "Action": {
    "Block": {}
  },
  "VisibilityConfig": {
    "SampledRequestsEnabled": true,
    "CloudWatchMetricsEnabled": true,
    "MetricName": "TestRule"
  },
  "Statement": {
    "AndStatement": {
      "Statements": [
        {
          "GeoMatchStatement": {
            "CountryCodes": [
              "KR"
            ]
          }
        },
        {
          "OrStatement": {
            "Statements": [
              {
                "SizeConstraintStatement": {
                  "FieldToMatch": {
                    "Body": {}
                  },
                  "ComparisonOperator": "GT",
                  "Size": 100,
                  "TextTransformations": [
                    {
                      "Priority": 0,
                      "Type": "NONE"
                    }
                  ]
                }
              },
              {
                "ByteMatchStatement": {
                  "SearchString": "bot",
                  "FieldToMatch": {
                    "SingleHeader": {
                      "Name": "x-value"
                    }
                  },
                  "TextTransformations": [
                    {
                      "Priority": 0,
                      "Type": "LOWERCASE"
                    }
                  ],
                  "PositionalConstraint": "EXACTLY"
                }
              }
            ]
          }
        }
      ]
    }
  }
}

```
{{% /expand %}}

### 적용한 Rule 테스트

좀 더 다양한 파라미터를 전달할 수 있도록 CLI 를 사용하겠습니다. 

- 사용하고 계시는 PC의 Terminal로 접속합니다. 

{{% notice info %}}
가이드는 MAC OS 기반으로 작성되었습니다. 하지만 다른 OS에서도 동일하게 적용됩니다. 
{{% /notice %}}

- 우선 편의를 위해 DVWA 웹의 endpoint 값을 변수로 export 합니다. endpoint값은 모듈 1에서 생성한 CloudFormation Stack "MyDVWA"의 **Output** 탭에서 찾을 수 있는 "AlbEndpoint" 값입니다. 

```
export waflab_url=<your AlbEndpoint form CloudFormation stack>
```

- 공격자를 가장하여 다음과 같은 요청을 보내봅니다. 

```
# Blocked (header string match conddition)
curl -i -H "x-value: bot" $waflab_url

# Blocked (request body size condition)
curl -i -X POST -d "Amazon":"30","is":"12374934237","known":"Target 3","as":null,"one":"Configuration Deneme 3","of":null,"the":"Configuration Deneme 3","most":0,"customer-centric":3,"companies":true $waflab_url
```

- 다음과 같을 때는 정상 요청으로 판단되어 요청이 허용됩니다. 
```
# Allowed (header string match conddition & request body size condition)
curl -i -H "x-value: notbot" -X POST -d "valid":"size" $waflab_url
```


{{% notice info %}}
이번 실습의 Rule은 한국의 요청에 한해 조건들을 적용시키기 때문에 다른 국가에서 요청을 보내게 되면 어떤 룰도 차단되지 않는 것이 정상입니다. 
의도한대로 차단 혹은 허용이 되지 않는다면 현재 VPN이나 다른 국가의 EC2에서 요청을 보내고 있는지 확인해보시기 바랍니다. 
{{% /notice %}}




