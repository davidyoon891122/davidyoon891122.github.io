1. 파일 업로드 프로그래밍
- www.servlets.com 에서 COS library 다운받아 WebContent/WEB-INF/lib 에 넣어줌.
- <form action="fileFormOk.jsp" method="post" enctype="multipart/form-data">
	파일 : <input type="file" name="file"> <br/>
	<input type="submit" value="File Upload">
  </form>
- enctype속성 multipart/form-data 넣어야 서버로 파일 전송 가능
- <%
	String path = request.getRealPath("fileFolder");  // path to save files
	
	int size = 1024 * 1024 * 10; // 10M   
	String file = "";  
	String oriFile = "";
	
	try{
		MultipartRequest multi = new MultipartRequest(request, path, size, "EUC-KR", new DefaultFileRenamePolicy()); //DefaultFileRenamePolicy 동일 이름 있을 때 뒤에 숫자 추가 해주는 정책.
		
		Enumeration files = multi.getFileNames();
		String str = (String) files.nextElement();
		
		file = multi.getFilesystemName(str);
		oriFile = multi.getOriginalFileName(str); //실제 파일 이름
	} catch(Exception ex){
		ex.printStackTrace();
	}

%>

- 실제 파일일 저장되는 경로는 tomcat folder/stpwebapps/projectname/fileFolder
