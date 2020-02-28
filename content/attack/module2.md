+++
title = "XSS Exploit"
weight = 2
pre = "<b>2.2 </b>"
+++

* * *

  실제로 발생하는 다양한 웹 서비스 공격방식 중 하나인 XSS Exploit 공격을 진행하도록 하겠습니다. 
  
  
- XSS Exploit 공격을 진행하기 위하여 DVWA 메뉴에서 아래와 같이 "XSS(Reflected)" 메뉴를 클릭한 후 우측의 "User ID" 를 입력하는 화면에서 아래의 XSS 코드를 입력한 후 "Submit" 버튼을 클릭합니다.

```
<script>alert(document.cookie)</script>
```

![XSS Exploit](/images/DVWA_xss1.png)

- "Submit" 버튼을 클릭하면 아래와 같이 경고창이 나타나며 경고창에는 쿠키 정보가 포함되어 있는 것을 확인할 수 있습니다. 이 경고창은 조금 전 입력한 XSS 코드에 의하여 생성된 것으로 취약한 시스템에서의 쿠키 정보를 탈취하는 것을 손쉽게 시연하기 위하여 경고창이 사용되었습니다.

![XSS Exploit](/images/DVWA_xss2.png)

- 경고창의 "OK" 버튼을 클릭하면 아래와 같이 XSS (Reflected)화면에 Hello 라는 문자가 출력된 것을 확인할 수 있습니다.

![XSS Exploit](/images/DVWA_xss3.png)

 참고로 DVWA 웹페이지의 XSS(Reflected)취약점에 적용된 소스코드는 다음과 같습니다.
 
```
<?php

header ("X-XSS-Protection: 0");

// Is there any input?
if( array_key_exists( "name", $_GET ) && $_GET[ 'name' ] != NULL ) {
    // Feedback for end user
    echo '<pre>Hello ' . $_GET[ 'name' ] . '</pre>';
}

?>
```

 {{% notice warning %}}
 본 실습에서 사용한 SQL 구문은 XSS 공격에 사용되는 가장 기본적인 구문 중 하나입니다. 현재 사용되는 대부분의 웹 서비스는 이와 같은 간단한 XSS 코드에 대해서는 취약점이 없을 것으로 예상되지만 테스트 목적 이외의  악의적인 사용해서는 안되며 해당 행위로 인한 책임은 사용자에게 있음을 밝힙니다.
{{% /notice %}}
