# Salesforce_Develop
<h3>|Apex</h3>
Apex는 Java와 유사, 데이터베이스 저장 프로시저와 같이 작동하는 프로그래밍 언어.<br>
Apex를 통해 버튼 클릭, 관련 레코드 업데이트 및 Visualforce 페이지와 같은 시스템 이벤트에 비즈니스 논리 추가가능.
<br>
<h3>|Apex Trigger</h3>
<h6>1. System.debug() simply “prints” the value of anything you put inside it.</h6>
-Before triggers - 데이터베이스에 저장하기 전에 레코드 값을 업데이트하거나 유효성을 검사하는 데 사용<br>
-After triggers - 시스템에서 설정한 필드 값(예: 레코드의 ID 또는 LastModifiedDate 필드)에 액세스 및 다른 레코드의 변경 사항에 영향을 미치는 데 사용됩니다. after trigger가 발생한 레코드는 읽기 전용
<br><br>
<h6>2. Trigger Exception </h6>
 특정 조건이 충족되면 레코드가 저장되지 않도록 하는 등 특정 데이터베이스 작업에 대한 제한을 추가해야 하는 경우 <br>
 문제가 되는 sObject에 대한 addError() 메서드를 호출 <br>
 addError() 메서드는 트리거 내부에서 치명적인 오류를 발생시키고, 오류 메시지는 사용자 인터페이스에 표시되고 기록 <br>
 ex) Account에 관련 Opportunity가 있으면 Trigger를 통해 해당 Account 삭제 방지해야
<h6>3. Callout = 외부 웹 서비스에 대한 Apex 호출 </h6>
 Apex에서는 외부 웹 서비스를 호출하고 Apex 코드를 외부 웹 서비스와 통합 가능. <br>
ex)주식 시세 서비스에 콜아웃을 만들어 최신 시세 얻어오기 <br><br>
 트리거에서 호출할 경우 호출은 트리거 프로세스가 외부 서비스의 응답을 기다리는 동안 작업을 차단하지 않도록 비동기적으로 수행되어야 함 <br>
비동기 호출은 백그라운드 프로세스에서 수행, 외부 서비스를 반환할 경우 응답이 수신됨.
<br>
<h3>|Apex Trigger Test</h3>

<h3>|에러 해결</h3>
1. The nonstatic method cannot be referenced from a static context.<br>
-Change the method to static <br>
-Address the non-static variable with the object name
