1. url-pattern
- 디렉터리 패턴
    - 디렉터리 형태로 서버의 해당 컴포넌트를 찾아서 실행하는 구조
    - http://localhost:8181/exampleProject/Hello -> /Hello Servlet
    - 서블릿 이름으로 각각 찾아서 이동
- 확장자 패턴
    - 확장자 형태로 서버의 해당 컴포넌트를 찾아서 실행하는 구조
    - http://localhost:8181/exampleProject/hello.do -> *.do Servlet
    - .do로 끝나는 요청들은 Servlet으로 가서 hello.do, world.do 각각의 요청에 따라 처리

2. FrontController 패턴
- 클라이언트의 다양한 요청을 한곳으로 집중시켜, 개발 및 유지보수에 효율성을 극대화 한다.
- 요청_1 -> 요청 1 처리 서블릿 -> DAO
  요청_2 -> 요청 2 처리 서블릿 -> DAO
  요청_3 -> 요청 3 처리 서블릿 -> DAO

- 요청 1
  요청 2  -> 모든 요청을 처리하는 서블릿 -> DAO
  요청 3

3. Command Pattern
- 클라이언트로부터 받은 요청들에 대해서, 서블릿이 작업을 직접 처리 하지 않고, 해당 클래스가 처리하도록 하는 패턴
- 요청 1
  요청 2 -> 모든 요청을 처리하는 서블릿 -> DAO
  요청 3 
                                                      interface
- 요청 1                                        -> 요청1 처리 클래스
  요청 2 -> 모든 요청을 직접 처리하지 않는 서블릿  -> 요청2 처리 클래스 -> DAO
  요청 3                                        -> 요청3 처리 클래스

- FrontController
    - 
    package userverify;
    import java.io.IOException;
    import java.io.PrintWriter;
    import java.security.Timestamp;
    import java.util.ArrayList;

    import javax.servlet.ServletException;
    import javax.servlet.annotation.WebServlet;
    import javax.servlet.http.HttpServlet;
    import javax.servlet.http.HttpServletRequest;
    import javax.servlet.http.HttpServletResponse;

    /**
    * Servlet implementation class FrontCon
    */
    @WebServlet("*.do")
    public class FrontCon extends HttpServlet {
        private static final long serialVersionUID = 1L;
        
        /**
        * @see HttpServlet#HttpServlet()
        */
        public FrontCon() {
            super();
            // TODO Auto-generated constructor stub
        }

        /**
        * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse response)
        */
        protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
            // TODO Auto-generated method stub
            response.getWriter().append("Served at: ").append(request.getContextPath());
            actionDo(request, response);
        }

        /**
        * @see HttpServlet#doPost(HttpServletRequest request, HttpServletResponse response)
        */
        protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
            // TODO Auto-generated method stub
            doGet(request, response);
            actionDo(request, response);
        }

        private void actionDo(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
            System.out.println("actionDo()");
            
            String uri = request.getRequestURI();
            String conPath = request.getContextPath();
            String command = uri.substring(conPath.length());
            
            if(command.equals("/membersAll.do")) {
                response.setContentType("text/html;charset=EUC-KR");
                PrintWriter writer = response.getWriter();
                writer.println("<html><head></head><body>");
                
                Service service = new MembersAllService();
                ArrayList<MemberDto> dtos = service.execute(request,response);
                
                for(int i = 0; i< dtos.size(); i++) {
                    MemberDto dto = dtos.get(i);
                    String id = dto.getId();
                    String pw = dto.getPw();
                    String name = dto.getName();
                    String eMail = dto.geteMail();
                    java.sql.Timestamp rDate = dto.getrDate();
                    String address = dto.getAddress();
                    
                    writer.println(id + "," + pw + ", " + name + ", " + eMail + ", " + rDate + ", " + address + "<hr/>");
                    
                }
                writer.println("</body></head>");
            } 
        }
        
    }

- Service Interface
    - 
        package userverify;

        import java.util.ArrayList;

        import javax.servlet.http.HttpServletRequest;
        import javax.servlet.http.HttpServletResponse;

        public interface Service {
            public ArrayList<MemberDto> execute(HttpServletRequest request, HttpServletResponse response);
        }

- MemebersAllService.java
    - 
    package userverify;

    import java.util.ArrayList;

    import javax.servlet.http.HttpServletRequest;
    import javax.servlet.http.HttpServletResponse;



    public class MembersAllService implements Service{

        public MembersAllService() {
            
        }
        
        public ArrayList<MemberDto> execute(HttpServletRequest request, HttpServletResponse response) {
            // TODO Auto-generated method stub
            
            MemberDao dao = MemberDao.getInstance();
            return dao.membersAll();

        }
    }

