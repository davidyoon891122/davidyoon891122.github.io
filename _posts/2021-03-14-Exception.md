1. 예외 페이지의 필요성
- JSP, Servlet에서 예외 발생
- 예외 상황에서 웹컨테이너(톰캣)에서 제공되는 기본적인 에외 페이지 보여줌
- 사용자 예외 페이지로 설정가능

2. page지시자를 이용한 예외 처리
- <%@ page errorPage="errorPage.jsp"%>
 <%
    int i = 40/0;
 %>

- errorPage.jsp
 <%@ page isErrorPage="true"%> -> true 값이어만 exceptio 관련 메소드 사용가능
 <% response.setStatus(200); %>
 <%= exception.getMessage() %>

3. web.xml파일을 이용한 예외 처리
- 
 <error-page>
 	<error-code>404</error-code>
 	<location>/error404.jsp</location>
 </error-page>
 <error-page>
 	<error-code>500</error-code>
 	<location>/error500.jsp</location>
 </error-page>

-