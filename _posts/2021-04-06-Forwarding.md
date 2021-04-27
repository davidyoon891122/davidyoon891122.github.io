1. RequestDispatcher 클래스
- Servlet 또는 JSP에서 요청을 받은 후 다른 컴포넌트로 요청을 위임 할 수 있다.
- 이러한 위임 방법에는 2개의 클래스를 이용
- RequestDispatcher, HttpServletResponse
- RequestDispatcher 클래스의 경우 요청 받은 요청객체(request)를 위임받는 컴포넌트에 동일하게 전달 할 수 있다.
- RequestDispatcher 클래스
    - 클라이언트 요청(request객체) -> 요청받은 컴포넌트 요청위임(request 객체) -> 위임받은 컴포넌트
- dispatcher.jsp
   - <%@ page language="java" contentType="text/html; charset=EUC-KR"
    pageEncoding="EUC-KR"%>
    <!DOCTYPE html>
    <html>
    <head>
    <meta charset="EUC-KR">
    <title>Insert title here</title>
    </head>
    <body>
        dispatcherJsp.jsp
        <hr/>
        id : <%= request.getAttribute("id") %> <br/>
        pw : <%= request.getAttribute("pw") %>
    </body>
    </html>

- RequestObj.java(servlet)
    - private void actionDo(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		System.out.println("actionDo()");
		
		request.setAttribute("id", "abcde");
		request.setAttribute("pw", "12345");
		
		RequestDispatcher dispatcher = request.getRequestDispatcher("/dispatcher.jsp");
		dispatcher.forward(request, response);
	    }


2. HttpServletResponse 클래스
- 요청 받은 요청객체를 위임 받은 컴포넌트에 전달 하는 것이 아닌, 새로운 요청객체를 생성한다
- HttpServletResponse 클래스
    - 클라이언트 요청 -> 요청받은 컴포넌트
                    <- 응답
    클라이언트 요청 -> 위임받은 컴포넌트
                   <- 응답
    - request 객체가 달라진다
- 이거 이해 안되어 다시 확인 필요! 
- 클라이언트 -> 요청 -> 요청컴포넌트 -> 응답 -> 클라이언트 -> 요청 -> 위임받은 컴포넌트 -> 응답