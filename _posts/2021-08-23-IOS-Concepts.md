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

