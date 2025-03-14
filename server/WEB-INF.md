## WEB-INF와 404 Error와의 관계
최근 Servlet/JSP 수업 내용을 복습하기위해 노트북으로 프로젝트를 실행하면 계속 브라우저 404 Error로 고생을 있었다.
드디어 에러를 해결하게되어 깨달은 내용을 적어본다.
<img width="807" alt="Image" src="https://github.com/user-attachments/assets/48a2d86a-c531-4fc4-a7bb-a443bf1c79e6" />
<img width="277" alt="Image" src="https://github.com/user-attachments/assets/af7468f2-b68d-4179-8feb-b62425de7de8" />

1. web-app폴더에 파일이 있을 경우 비즈니스 로직(Controller)없이도 tomcat을 이용하여 브라우저 호출이 바로 되었고 뷰를 확인할 수 있다.
2. web-app > WEB-INF에 저장된 파일의 경우에는 직접적으로 접근이 불가한 경로로 보안 또는 유저에게 공개가 불필요한 정보를 저장하며 Controller를 통해서만
접근이 가능하다.

따라서 유저에게 공개되도 상관없고 보안이 필요없는 정보라면 wep-app 폴더에 직접 저장해도 상관없지만 보안이 필요하거나 우리가 진행하는 프로젝트의 경우에는 WEB-INF
에 저장해서 관리하는것이 좋다.

---
따라서 직접 접근이 아닌 .do를 통하여 접근하는 방식으로 404에러를 해결하였다.
```java
@WebServlet("/ex02.do")
public class Ex02 extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

        //Ex02.java
        String word = req.getParameter("word");
        String page = req.getParameter("page"); 
        
        if (word != null) {
            //검색 > doPost 하던일
            BookDAO dao = new BookDAO();
            ArrayList<BookDTO> list = dao.search(word, page);
            int total = dao.getTotal(word);
            
            req.setAttribute("list", list);
            req.setAttribute("word", word); 
            req.setAttribute("page", page);
            req.setAttribute("total", total);
            
        } else {
            req.setAttribute("page", "1");
        }
        
        req.getRequestDispatcher("/WEB-INF/views/data/ex02.jsp").forward(req, resp);
    }
```

### 레퍼런스
https://xzio.tistory.com/1345
https://kimsg.tistory.com/165
