1. 액션태그란
- JSP 페이지 내에서 어떤 동작을 하도록 지시하는 태그
- 페이지 이동, 페이지 include 등
- Bean 관련된 태그도 있음

2. forward, include, param 태그
- forward
    - 현재의 페이지에서 다른 특정페이지로 전환할 때 사용
    - <jsp:forward page="sub.jsp"/>
- include
    - 현재 페이지에 다른 페이지를 삽입할 때 사용
    - <jsp:include page="include02.jsp" flush="true">
- param
    - forward 및 include 태그에 데이터 전달을 목적으로 사용되는 태그
    - 이름과 값으로 이루어져 있다.
    - <jsp:forward page="forward_param.jsp>
        <jsp:param name="id" value="abcdef"/>
        <jsp:param name="pw" value="1234"/>
       </jsp:forward>
    - in forward_param.jsp
    