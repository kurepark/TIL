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


```
	<form action="PostMethod" method="post"> <!-- form태그에서 method가 post방식으로 action의 PostMethod라는 서블릿으로 찾아간다(PostMethod.java를 찾아감) -->
		<input type="submit" value="post">
	</form>

```     


- 컨텍스트 패스(context path) : WAS(Web Application Server)에서 웹어플리케이션을 구분하기 위한 path. 이클립스에서 프로젝트를 생성하면 자동으로 servers폴더에 tomcat~폴더에 server.xml에 추가 됩니다.

- servlet 작동순서 : 클라이언트에서 서블릿 요청이 들어 오면 서버에서는 서블릿 컨테이너를 만들고, 요청이 있을 때마다 스레드가 생성 된다		
웹브라우저 -> 웹서버 -> 웹어플리케이션 서버 -> 서블릿 컨테이너(1. 스레드생성, 2. 서블릿객체 생성)

- 서블릿 라이프사이클(생명주기)
	- 서블릿의 사용도가 높은 이유는 빠른 응답 속도 때문
	- 서블릿은 최초 요청 시 객체가 만들어져 메모리에 로딩되고, 이후 요청 시에는 기존의 객체를 재활용하므로 속도가 빠르다.
```
서블릿 객체생성 - 최초한번
	|	----------> 선처리 @PostConstruct
   Init() 호출 - 최초한번
	|
service(), doGet(),doPost() 호출 - 요청시 매번
	|
destroy() 호출 -  마지막 한번(자원 해제 : 서블릿 수정, 서버 재가동 등)	
	|	--------> 후처리 @PreDestroy\
	
- 서블릿 선처리, 후처리 : 서블릿의 라이프 사이클 중 init()과 destroy()메소드와 관련하여 선처리	(init()이전)와 후처리(destroy()후) 작업이 가능하다
```


#### form 태그 - 180630
- input 속성
	1. type : 태그 종류 지정
	2. name : input태그 이름
	3. value : name에 해당하는 값(name = value)

```
<form action = "FormEx" method="post">
action : 요청하는 컴포넌트 이름(찾아갈 파일)
method : 요청을 처리하는 방식(get / post)

get방식 : url에 정보가 모두 표현됨
post방식 : 보안에 강하다
```	
form태그의 submit버튼을 클릭해 데이터를 서버로 전송하면, 해당파일(servlet)에서는 HttpServletRequest객체를 이용하여 파라미터값을 얻을 수 있다.		
- getParameter(name) : 해당하는 name의 value 값을 준다
- getParameterValues(name) : 체크박스처럼 값이 여러개일 때
- getParameterNames() : 폼태그안에 있는 name을 배열로

```
<form action="FormEx" method="post">
	이름 : <input type="text" name="name">
	아이디 : <input type="text" name="id"> 
	비밀번호 : <input type="password" name="pw"> 
</form>

---------
String id = request.getParameter("id"); //사용자가 입력한 아이디 입력값
String pw = request.getParameter("pw"); //사용자가 입력한 비밀번호 입력값
```
한글처리 : 톰캣 서버의 기본 문자 처리 방식은 **IOS-8859-1** 이므로 별도의 한글 인코딩을 하지 않으면 한글이 깨져보인다. GET방식과 POST방식에 따라 한글처리 방식이 다르다		

GET방식 : <server.xml> 수정
```
<Connector URIEncoding = "EUC-KR" port="8181">
```
POST방식 : <request.setCharacterEncoding()> 메소드 이용
```
request.setCharacterEncoding("EUC-KR");
```

서블릿 초기화 파라미터 : ServletConfig		
**특정 서블릿**이 생성될 때 초기에 필요한 데이터들을 미리 설정해서 사용할수 있는 데이터들을 초기화 파라미터라고 한다. web.xml에 기술하고, 서블릿에서는 sevletConfig 클래스를 이용해서 접근한다. 초기화 파라미터를 web.xml이 아닌 sevlet파일에 직접 기술하는 방법도 있다.		

1. web.xml파일에 초기화 파라미터 기술
	1. 서블릿 클래스 제작
	2. web.xml파일에 초기화 파라미터 기술
	3. SevletConfig 메소드 이용해서 데이터 불러오기
2. 서블릿 파일에초기화 파라미터 기술
	1. 서블릿 클래스 제작
	2. @WebInitParam에 초기화 마라미터 기술
	3. SevletConfig 메소드 이용해서 데이터 불러오기


데이터 공유 : SevletContext		
여러 서블릿에서 특정 데이터를 공유해야할 경우 context parameter를 이용해서 web.xml에 데이터를 기술하고 서블릿에서 공유하면서 사용 할 수 있다.

1. 서블릿 클래스 제작
2. web.xml파일에 context parameter기술
3. ServletContext 메소드를 이용해서 데이터를 불러오기

웹어플리케이션 감시 : SevletContextListener		
웹 어플리케이션의 생명주기를 감시하는 리스너. 리스너의 해당 메소드가 웹 어플리케이션의 시작과 종료 시 호출 된다.(contextInitialized(), contextDestroyed())

1. 리스너 클래스 제작
2. web.xml파일에 리스너 클래스 기술	

