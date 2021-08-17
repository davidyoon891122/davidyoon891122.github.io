### Memory
1. Automatic Reference Counting
+ Reference 타입(class)은 heap 메모리에 저장된다 
+ 메모리는 자동으로 관리된다
+ 가르키는 포인터의 카운터를 세다가 0이되면 놓아버리는 형식의 메모리 관리

2. ARC에 영향을 주는 세가지
+ strong
    * 디폴트 
    * 레퍼런스 카운트 증가(선언된 변수가 힙에 머물도록 하는 타입)
+ weak
    * 메모리에 참조되어 있는 값이 없다면 nil로 만드는 타입
    * 힙에 있는 무엇가를 가르키고 있지만 관심이 없어서 사라져버리면 nil로 설정
    * nil로 설정 가능하다는 것은 optional 포인터여야만 한다는 의미
    * 대표적인 예로 UILabel을 보여주기 위한 Outlet등이 있다.
+ unowned
    * 참조 횟수를 세지마라는 의미
    * 가르키는 값이 사라지면 크래쉬 발생


### Closures
1. Capturing
+ 클로저는 Heap 메모리에서 사용 되고, 레퍼런스 타입이다.
+ 클로저는 클로저를 둘러쌓고 있는 변수들을 사용할 수 있고 이 captured 변수들은 클로저가 heap에 머무는 동안 함께 머물게 된다.
+ 이것은 메모리 사이클을 만들 수 있음
+ 메모리 사이클이란
    * 클로저가 어떤 객체를 가르키고, 객체도 클로저를 가르키게 된다면 서로 가르키게 되고 순환 참조가 발생하게 된다
    * addUnaryOperation("루트") { [self weakSelf = self] in
        weakSelf?.display.textColor = UIColor.redColor()
        return sqrt($0)
    }


### Extensions
1. Extensions
+ 메소드나 프로퍼티를 다른 클래스에게 추가하게 해줌
+ class, struct, enum 모두 사용 가능
+ 이제 존재하는 메소드를 다시 구현할 수는 없다
+ 추가된 요소들은 계산된 요소여야만 한다

### Protocol
1. protocols
+ API를 더욱 간결하게 표현하는 방법
+ 선언된 메소드와 프로퍼티들로 된 집합체
+ 프로토콜은 타입이다
+ 프로토콜을 실행하는 class, struct, enum에서 사용 가능
+ extension을 사용할 수 있음

2. four aspects
+ protocol declaration
    * 프로토콜에 들어갈 메소드와 프로퍼티를 선언하는 작업
+ class, struct, enum이 자기가 이 프로토콜을 실행하겠다고 선언
+ 프로토콜에 있는 값들을 구현하고 실행
+ 프로토콜을 실행한다면, 프로토콜에 있는 모든 것들을 실행해야함
    * ObjectiveC에서는 optional을 통해 필요한 것만 구현 가능
    * @objc protocol로 objectiveC버전으로 프로토콜 실행가능
    * optional 키워드로 func 나 var 앞에 붙일 수 있음
    * optional 프로토콜을 실행하는 클래스는 NSObject를 상속 받아야만 한다.
+ 프로토콜은 다중 상속 받을 수 있음
    * 상속 받은 프로토콜의 모든 것들을 실행해야한다.
+ var 에 get 이나 get and set 설정 해주어야 함
+ 변경될 예정인 함수들은 mutating 키워드 붙어야함 (struct(값 타입)에 변경이 발생하는 경우)
+ protocol Somprotocol: class 하면 class만 해당 프로토콜 상속 가능
+ 프로토콜 안에 initializer 사용 가능
+ 프로토콜 안에 init이 있고 클래스가 그것을 실행한다면 그 init을 required로 만들어야 한다.
+ extension에 추가 가능 