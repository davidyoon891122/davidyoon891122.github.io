1. DAO, DTO
- DAO
    - Data Access Object
    - 데이터 베이스에 접속해서 데이터 추가, 삭제, 수정 등의 작업을 하는 클래스
    - 일반적인 JSP 혹은 Servlet 페이지내에 위에 로직을 함께 기술할 수 도 있음
    - 유지보수 및 코드의 모듈화를 위해 별도의 DAO 클래스를 만들어 사용.
    - DataBase 설정에 관련된 셋팅 및 DTO객체에 Database에서 가져온 데이터 넣어주는 해주는 작업
    - 
    package daodto;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;
import java.util.ArrayList;

public class MemberDAO {

	private String url = "jdbc:oracle:thin:@localhost:1521:xe";
	private String uid = "c##davidyoon";
	private String upw = "DBPASS";
	
	public MemberDAO() {
		try {
			Class.forName("oracle.jdbc.driver.OracleDriver");
		} catch(Exception e) {
			e.printStackTrace();
		}
	}
	
	
	public ArrayList<MemberDTO> memberSelect() {
		ArrayList<MemberDTO> dtos = new ArrayList<MemberDTO>();
		
		Connection connection = null;
		Statement stmt = null;
		ResultSet resultSet = null;
		
		try {
			connection = DriverManager.getConnection(url, uid, upw);
			stmt = connection.createStatement();
			resultSet = stmt.executeQuery("select * from member");
			
			while(resultSet.next()) {
				String name = resultSet.getString("name");
				String id = resultSet.getString("id");
				String pw = resultSet.getString("pw");
				String phone1 = resultSet.getString("phone1");
				String phone2 = resultSet.getString("phone2");
				String phone3 = resultSet.getString("phone3");
				String gender = resultSet.getString("gender");
				
				MemberDTO dto = new MemberDTO(name, id, pw, phone1, phone2, phone3, gender);
				
				dtos.add(dto);
			}
			
		}catch(Exception e) {
			e.printStackTrace();
		}
		
		return dtos;
		
	}
}


- DTO
    - Data Tranfer Object
    - DAO클래스를 이용하여 데이터 베이스에서 데이터를 관리할 때 데이터를 일반적인 변수에 할당하여 작업할 수도 있지만, 해당 데이터의 클래스를 만들어 사용
    - DAO라는 클래스를 만들어 데이터 베이스에서 가져온 데이터들은 넣어 get set함수로 사용.
    - 
    package daodto;

public class MemberDTO {
	private String name;
	private String id;
	private String pw;
	private String phone1;
	private String phone2;
	private String phone3;
	private String gender;
	
	
	
	
	public MemberDTO(String name, String id, String pw, String phone1, String phone2, String phone3, String gender) {
		super();
		this.name = name;
		this.id = id;
		this.pw = pw;
		this.phone1 = phone1;
		this.phone2 = phone2;
		this.phone3 = phone3;
		this.gender = gender;
	}
	
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public String getId() {
		return id;
	}
	public void setId(String id) {
		this.id = id;
	}
	public String getPw() {
		return pw;
	}
	public void setPw(String pw) {
		this.pw = pw;
	}
	public String getPhone1() {
		return phone1;
	}
	public void setPhone1(String phone1) {
		this.phone1 = phone1;
	}
	public String getPhone2() {
		return phone2;
	}
	public void setPhone2(String phone2) {
		this.phone2 = phone2;
	}
	public String getPhone3() {
		return phone3;
	}
	public void setPhone3(String phone3) {
		this.phone3 = phone3;
	}
	public String getGender() {
		return gender;
	}
	public void setGender(String gender) {
		this.gender = gender;
	}
	
	
}




- 웹브라우저 -> 서버( Servlet/JSP <-> DAO <-> DTO) -> DataBase

2. PreparedStatement객체
- SQL문을 실행하기 위해 Statement 객체 이용
- Statement 객체의 경우 중복코드가 많아지는 단점
- 
 	public void memberUpdate(Member member) {
		try {
			connection = DriverManager.getConnection(url, uid, upw);
			String query = "insert into memberforpre (id, pw, name, phone) values(?, ?, ?, ?)";
			int n;
			pstmt = connection.prepareStatement(query);
			
			pstmt.setString(1, member.getId());
			pstmt.setString(2, member.getPw());
			pstmt.setString(3, member.getName());
			pstmt.setString(4, member.getPhone());
			n = pstmt.executeUpdate();
		
			if (n == 1) {
				System.out.println("insert success");
			}else {
				System.out.println("insert fail");
			}
			
		} catch (SQLException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} finally {
			try {
				if(connection != null) connection.close();
				if(pstmt != null) pstmt.close();
			} catch (Exception e) {
				// TODO: handle exception
			}
		}
		
	}

3. 커넥션 풀(DBCP)
- 클라이언트 다수의 요청이 발생할 경우 데이터베이스에 부하 발생
- 이 문제를 해결하기 위해 커네션 풀 사용 (DataBase Connection Pool)
- 클라이언트가 요청전에 서버에서 미리 데이터베이스 객체를 여러개 생성하여 풀을 만들고 고객이 들어오면 해당 객체가 사용 되는 형식
- tomcat 컨테이너가 테이터베이스 인증을 하도록 context.xml 파일에 코드 추가
- 
	<Resource
		auth="Container"
		driverClassName="oracle.jdbc.driver.OracleDriver"
		url="jdbc:oracle:thin:@localhost:1532:xe"
		username="c##davidyoon"
		password="xxxx"
		name="jdbc/Oracle18g"
		type="javax.sql.DataSource"
		maxActive="50"  //풀 갯수
		maxWait="1000" // 다음 풀(51번째) 만들때 대기 시간
	/>