1. EL
- Expression Language란, 표현식 또는 액션 태그를 대신해서 값을 표현하는 언어
- <%= value %> 표현식, ${value} EL
- ${안에서 연산자 사용 가능}
- 	${1+2 } <br/> -> <%= 1+2 %>
	${1-2 } <br/>
	${1*2 } <br/>
	${1/2 } <br/>
	${1 <2 } <br/>
	${ 1 >2 } <br/>
	${(1>2)?1:2 } <br/>

2. 액션태그로 사용되는 EL
- <jsp:getProperty name="member" property="name"/>
- ${member.name}


3. 내장객체
- pageScope: page객체를 참조하는 객체
- requestScope: request 객체를 참조하는 객체
- sessionScope: session 객체를 참조하는 객체
- applicationScope: application 객체를 참조하는 객체
- param: 요청 파라미터를 참조하는 객체
- paramValues: 요청 파라미터(배열)을 참조하는 객체
- initParam: 초기화 파라미터를 참조하는 객체
- cookie: cookie 객체를 참조하는 객체
- 	<%
		String id = request.getParameter("id");
		String pw = request.getParameter("pw");
	%>
	
	아이디 : <%=id %> <br/>
	비밀번호 : <%=pw %> <br/>
	
	<hr/>
	
	아이디: ${param.id } <br/>
	비민번호: ${param.pw } <br/>
	아이디 : ${param["id"] } <br/>
	비밀번호 : ${param["pw"] } <br/>
	
	
	<hr/>
	
	applicationScope : ${applicationScope.application_name } <br/>
	sessionScope : ${sessionScope.session_name } <br/>
	pageScope : ${pageScope.page_name } <br/>
	requestScope : ${requestScope.request_name } <br/>
	
	<hr/>
	
	context 초기화 파라미터 <br/>
	${initParam.con_name } <br/>
	${initParam.con_id } <br/>
	${initParam.con_pw } <br/>