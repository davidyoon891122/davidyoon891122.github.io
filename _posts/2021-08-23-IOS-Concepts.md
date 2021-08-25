### IOS 개념 정리 
1. lazy var 란
+ 변수이지만 이 변수가 사용되거나, 호출되기전까지 초기화되지 않고 메모리 할당을 받지 않는 변수
+ 즉, 이 lazy 변수는 view controller가 초기화 되었을때 초기화되지 않는다.
+ 자신이 사용될떄가지 대기하다가 자신이 사용될 때 초기화 된다.
+ UI 구성요성을 초기화 할 때 유용하다.

2. UITextField 수직 정렬
+ textField.centerVerticalAlignment = .top

3. clipToBounds
+ textField.clipToBounds = true -> "true일때 내용들과 서브뷰들은 뷰의 테두리를 기준으로 잘리게 된다.

4. masksToBounds
+ layer 속성 이며, clipToBounds 와 똑같은 역할 내용들 테두리에 맞추어 자를지 말지 true false로 결정
+ textFeild.layer.masksToBounds = true -> "true일때 내용물과 서브뷰들은 testField의 테두리를 기준으로 잘리게 된다.

5. UI 세팅
+ ViewController에서 뷰를 그리지 말고 UIView로 View를 만들어서 ViewController에서 사용
+ updateConstrains() 함수 사용하여 UIView 레이아웃 설정
+ ViewCOntroller에서 세팅
    * lazy var mainView: MainView = {
        return MainView(tableView: self.tableView)
    }()
    * view.addSubview(mainView)
    * 레이아웃 설정

6. TableView 유동적인 행 높이 지정
+ 같은 Cell - 다른 높이 -> 같은 형태의 Cell을 사용하더라도 들어가는 컨텐츠의 내용이 다를 경우 높이가 다르게 될 수 있음
+ 이러한 형태를 고려하여 Cell 안에 요소들의 Constrains를 잘 지정해주어야 함
+ 스토리보드에서 테이블 Cell 높이를 지정할 떄 주의할 점은 Dynamic Prototype Cell을 만드는 경우에 TableView의 Row Height는 Cell의 Custom Row Height를 Override 한다
    * 즉, cell 높이를 500으로 지정해도, TableView에서 Row Height 값이 50이면 50으로 적용된다는 뜻
    * static cell인 경우는 Cell의 높이가 row height보다 우선시 된다.
+ AutomaticDimension
    * 가각 다른 cell마다 높이를 적용하는 것이라면 tableView 메소드 중 HeightForRowAtIndexPath를 사용하여 임의로 해당 Cell 높이 지정 가능
    * 하지만 같은 cell의 높이를 각각 지정하려면 AutomationDimension을 통해 테이블 Row의 높이가 유동적이라고 선언해야 한다.
    * 이 선언을 통해 위에서 지정한 row height는 무시되고 row안의 내용에 따라 row의 높이가 유동적으로 결정된다
    * tableView.rowHeight = UITableView.automaticDimension (최신 버전에서 변경됨)
+ estimatedRowHeight
    * 개발자가 예상되는 RowHeight 값
    * 테이블 뷰의 데이터가 Reload 될때 각 Row마다 대략적인 높이를 계산하는데 도움을 주는 역할
    * 직접대입, 메소드 사용 둘다 가능

7. 여러 뷰에서 데이터 공유
+ delegate 패턴 사용
    * A class에서 사용되는 데이터를 B class에서 가공하여 다시 A에서 사용하고 싶을때
    * protocol 정의
        + protocol TodoProtocol {
            func addTodoList(todoViewModel: TodoViewModel)
        }
    * A class에서 prococol implement
        + class A: TodoProtocol
        {
            func addTodoList(todoViewModel: TodoViewModel)
            {
                self.todoVM = TodoViewModel
            }
        }
    * A class init에서 B class delegate 변수 self 선언
        + init() {
            b.delegate = self
        }
    * B class에서 delegate 변수 선언
        + var delegate: TodoProtocol?
    * B class에서 delegate?.addTodoList(todoViewModel: self.TodoViewModel)