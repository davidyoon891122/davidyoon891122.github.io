---
layout: post
title:  "JSP Servlet"
categories: Web
---

JSP Servlet

Ch1. 웹 프로그래밍
-인터넷이란: 1개 이상의 네트워크가 연결되어 있는 형태
-http(Hyper Text Transfer Protocol)
-웹 프로그램의 동작
- 클라이언트 → 웹서버 → 웹어플리케이션서버(WAS) → 데이터베이스

Ch2. 설치
- Apache Tomcat 7.0
- Eclipse 설치 → 인텔리J 무료판은 구성하는 방법 모르겠음 tomcat쪽이 안나옴.

Ch3. JSP
-JSP 특징: 
	-동적 웹어플리케이션 컴포넌트
	-.jsp 확장자
	-클라이너트 요청에 동적으로 작동하고, 응답은 html을 이용
	-jsp는 서블릿으로 변환되어 실행
	-MVC 패턴에서 View로 이용됨
	-JSP(View), Servlet(Controller), DB(Model)

-아키텍처
.jsp file(Java 파일로 변환) → Java file(helloworld_jsp.java)(컴파일) → class file(helloworld_jsp.class)

-jsp 파일을 가져다가 html로 만듬.

Ch4. Servlet
- 특징
	- 동적 웹 어플리케이션 컴포넌트
	- .java 파일
	- 클라이언트에 요청에 동적으로 작동, 응답은 html 이용
	- java thread 이용 하여 동작
	- MVC패턴에서 Controller로 이용됨

- servlet 은 HttpServlet 상속 받음
- doGet, doPost 메소드 사용
- localhost:8181/servlet/com.javalec.ex.HW 하면 보안상 문제 or 편의상 좋지 않아서 web.xml 에서 맵핑 하거나, 어노테이션으로 맵핑

Ch.5 Servlet 
- Servlet(interface) → GenericServlet(abstract) → HttpServlet
- doGet(HttpServletRequest request, HttpServletResponse response)
- response.setContentType(“text/html”);
- PrintWriter writer = response.getWriter(); ← 웹브라우저 출력하기 위한 스트림
- write.println(“<html>”);
- request 객체에 정보가 담겨 웹서버로 전달, 받은 데이터를 확인하여 대응 되는 서비스 response 객체에 담아서 전달
- 요청방식
	-get: URL값으로 정보가 전송되어 보안에 약함 → doGet()함수가 처리
	-post: header를 이용해 정보가 전송되어 보안에 강함 → doPost() 함수가 처리
-doGet(): html내 form태그의 method 속성이 get일 경우 호출, 웹브라우저의 주소창을 이용하여 servlet을 요청한 경우에 호출
-doPost(): form태그 속성이 post일 경우 호출
-컨텍스트 패스(Context Path): WAS(Web Application Server)에서 웹어플리케ㅣ션을 구분하기 위한 path, 이클립스에서 프로젝트 생성하면 자동으로 server.xml에 추가 된다.

