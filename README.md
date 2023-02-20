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
1. Test class must start with @isTest annotation if class class version is more than 25.<br>
2. Test environment support @testVisible , @testSetUp as well.<br>
3. Unit test is to test particular piece of code working properly or not.<br>
4. Unit test method takes no argument, commit no data to database, send no email, flagged with testMethod keyword.<br>
5. To deploy to production at-least 75% code coverage is required. <br>
6. System.debug statement are not counted as a part of apex code limit.<br>
7. Test method and test classes are not counted as a part of code limit.<br>
9. We should not focus on the  percentage of code coverage, we should make sure that every use case should covered including positive, negative, bulk and single record .<br>
11 . @isTest annotation with test method  is equivalent to testMethod keyword.<br>
12. Test method should static and no void return type .<br>
13. Test class and method default access is private ,no matter to add access specifier .<br>
14. classes with @isTest annotation can't be a interface or enum .<br>
15. Test method code can't be invoked by non test request .<br>
16. Stating with salesforce API 28.0 test method can not reside inside non test classes .<br>
17. @Testvisible annotation to make visible private methods inside test classes.<br>
18. Test method can not be used to test web-service call out . Please use call out mock .<br>
19. You can't  send email from test method.<br>
20.User, profile, organization, AsyncApexjob, Corntrigger, RecordType, ApexClass, ApexComponent ,ApexPage we can access without (seeAllData=true) .<br>
21. SeeAllData=true will not work for API 23 version eailer .<br>
22. Accessing static resource test records in test class e,g List<Account> accList=Test.loadData(Account,SobjectType,'ResourceName').<br>
23. Create TestFactory class with @isTest annotation to exclude from organization code size limit .<br>
24. @testSetup to create test records once in a method  and use in every test method in the test class .<br>
25. We can run unit test by using Salesforce Standard UI,Force.com IDE ,Console ,API.<br>
26. Maximum number of test classes run per 24 hour of period is  not grater of 500 or 10 multiplication of test classes of your organization.<br>
27. As apex runs in system mode so the permission and record sharing are not taken into account . So we need to use system.runAs to enforce record sharing .<br>
28. System.runAs will not enforce user permission or field level permission .<br>
29. Every test to runAs count against the total number of DML issued in the process .<br>
<h3>|문제 해결 및 주의 사항</h3>
<br>
1. The nonstatic method cannot be referenced from a static context.<br>
-Change the method to static <br>
-Address the non-static variable with the object name<br>

2. date 필드에서 year만 추출<br>
date field -> YEAR(Field__c)<br>
date/time field -> YEAR(DATEVALUE(Field__c))<br>
To display it by itself -> need to be a number return type <br>
To make it back into a date -> need to use DATE (ex) DATE(YEAR(DATEVALUE(Field__c)), 1, 1 <br>

3. if you are creating trigger before insert or before update, then you should do changes on the trigger.new list only.
   Do not create another list for update.

4. Dependent class is invalid and needs recompilation <br>
Setup | Custom Code | Apex Classes -> Compile all classes <br>
Setup | Custom Code | Apex Triggers -> Compile all triggers <br>

5. A non foreign key field cannot be referenced in a path expression: AccountId <br>
Replace this line oppJobList.add(opp.AccountId.Name) <br>
with this code oppJobList.add(opp.Account.Name) <br>

6. Apex class에서 Date 변수값 설정<br>
Date d = Date.newInstance(2023.01.01) <br>
파라미터로 Date 넘길 때도, 변수 선언해서 전달

7. Access modifier <br>
Private :- This is the default and means that the method or variable is accessible only within the Apex. If you do not specify an access modifier, the method or variable is private. <br>
Protected :- This means that the method or variable is visible to any inner classes in the defining Apex class, and to the classes that extend the defining Apex class. You can only use this access modifier for instance methods and member variables. <br>
Public :- This means the method or variable can be used by any Apex in this application or namespace. <br>
global :- This means the method or variable can be used by any Apex code that has access to the class, not just the Apex code in the same application. This access modifier should be used for any method that needs to be referenced outside of the application, either in the SOAP API or by other Apex code. If you declare a method or variable as global, you must also declare the class that contains it as global. <br>
 
 8. Future Method <br>
Future method is used to run processes in a seperate thread. <br>
It must be static, only return void type. <br>
+)To test future methods, enclose your test code between the startTest() and stopTest() test methods. <br>
 
 9. Queueable Apex <br>
 functionally equivalent to future methods (어떤 때는 동기적으로 실행되고 어떤 때는 비동기적으로 실행될 경우, queueable보다 future method 사용) <br>
 
 10. Clone Method <br>
 clone(boolean preserveId, boolean isDeepClone, boolean preserveReadonlyTimestamps, boolean preserveAutonumber) <br>
<code>
 ex)
  public static void cloneRecord(){
        // retrive contact record for clone
        Contact con = [SELECT FirstName, Email, LastName FROM Contact LIMIT 1];
 
        // clone record
        Contact conCopy = con.clone(false, false, false, false);
        insert conCopy;
    }
 
 </code>
<hr>
<h3>|Lightning Web Component</h3>
[예시]<br>
CreateUser.cmp—The Lightning component that you see when you open the action. It contains the UI implementation, which includes the text fields, buttons, action title, and so on.<br>
CreateUserController.js—The controller that listens to the component and any UI events that take place, such as the initial load, text input, and button clicks. Its function is to delegate these events to the helper class, CreateUserHelper.js.<br>
CreateUserHelper.js—The code that deals with all the business logic, such as validating the password and email fields. <br>
