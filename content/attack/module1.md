+++
title = "SQL Injection"
weight = 1
pre = "<b>2.1 </b>"
+++

* * *

실제로 발생하는 다양한 웹 서비스 공격방식 중 하나인 SQL Injection 공격을 진행하도록 하겠습니다. 
  
- SQL Injection 공격을 진행하기 위하여 DVWA 메뉴에서 아래와 같이 "SQL Injectin" 메뉴를 클릭한 후 우측의 "User ID" 를 입력하는 화면에서 아래의 SQL 구문을 입력한 후 "Submit" 버튼을 클릭합니다.
  
  ```
  ' OR 1=1 #  
  ```
  
  {{% notice info %}}
 위 공격에 사용되는 특수문자는 "`" 입니다. 코드를 직접 입력했는데 공격이 성공되지 않으시는 분들은 위 코드를 그대로 복사하셔서 사용하시기 바랍니다. 
{{% /notice %}}

 
 ![DVWA Setting](/images/DVWA_sqlinjection1.png)

- "Submit" 버튼을 클릭한 후 아래 화면과 같이 여러가지 계정 정보가 출력되는 것을 확인합니다.
 ![DVWA Setting](/images/DVWA_sqlinjection2.png) 
 
 {{% notice warning %}}
 본 실습에서 사용한 SQL 구문은 SQL Injection 공격에 사용되는 가장 기본적인 구문 중 하나입니다. 현재 사용되는 대부분의 웹 서비스는 이와 같은 간단한 SQL 구문에 대해서는 취약점이 없을 것으로 예상되지만 테스트 목적 이외의  악의적인 사용해서는 안되며 해당 행위로 인한 책임은 사용자에게 있음을 밝힙니다.
{{% /notice %}}
