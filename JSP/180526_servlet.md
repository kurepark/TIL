### 인프런JSP - servlet
-----
servlet은 java언어를 사용하여 웹프로그램을 제작하는 것.         

클라이언트에서 웹어플리케이션으로 요청을 할때 request하는 방식이 두가지가 있다.         
html form태그의 method에서 방식을 정해준다.

- doGet방식 :  URL값으로 정보가 전송되어 보안에 약함 (Form 태그 method 속성값 = get)        
웹브라우저의 주소창을 이용하여 sevlet을 요청한 경우에도 호출이 된다.        
doGet 메소드는 매개변수로 HttpServletRequest와 HttpServletResponse를 받는다
    1. HttpServletRequest : 클라이언트의 요청처리 객체, setContentType()메소드를 호출하여 응답방식을 결정
    2. HttpServletResponse : 클라이언트에게 응답처리 객체, getWrite()메소드를 이용하여 출력 스트림을 얻는다. 출력스트림의 println()메소드를 이용하여 출력하면, 웹브라우저에 출력 된다

- doPost방식 : header를 이용해 정보가 전송되어 보안에 강함(Form 태그 method 속성값 = post) 
```
	<form action="PostMethod" method="post"> <!-- form태그에서 method가 post방식으로 action의 PostMethod라는 서블릿으로 찾아간다(PostMethod.java를 찾아감) -->
		<input type="submit" value="post">
	</form>

```     


- 컨텍스트 패스(context path) : WAS(Web Application Server)에서 웹어플리케이션을 구분하기 위한 path. 이클립스에서 프로젝트를 생성하면 자동으로 servers폴더에 tomcat~폴더에 server.xml에 추가 됩니다.
