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
+ protocol 과 extension은 저장 공간이 없다.
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

### Delegation
+ 프로토콜을 사용하는 대표적인 예
+ 델리게이션은 눈에 보이지 않는 소통을 하는 방식(blind communication between a View and Controller)
+ 프로토콜을 이용하여 델리게이션 하는 방법 
    * 뷰에서 델리게이션 프로토콜을 선언한다.
        - MainTableViewController: ToDoProtocol
    * 뷰의 API는 weak delegate를 가지고 있을 것이고 이것은 델이게이션 프로토콜 타입이다.
        - AddTodoViewController {
            weak var delegate: TodoProtocol?
        }
        - weak or unowned인 이유: 컨트롤러가 뷰를 메모리에 저장할 수 있지만, 뷰가 컨트롤러를 메모리에 저장하게 하고 싶진 않을테니까
        - 사용하지 않으면 nil로 초기화
    * 뷰가 delegate 사용: 뷰가 메시지를 보내길 원할 때
        - should, will, did, count, data ... etc 
    * 컨트롤러는 이 프로토콜을 실행한다고 선언한다
    * 컨트롤러는 자기자신(self)을 delegate라고 지정한다
        - addViewController.delegate = self
    * 컨트롤러는 프로토콜을 실행
+ 모든 델리게이트 들은 오프젝티브C로 구성되어 있어서 IOS의 대부분의 델리게이트(ScrollVeiwDelegate, TableViewDelegate)의 거의 모든 메소드들은 옵셔널이다.
+ 위에 과정을 걸치면 뷰는 컨트롤러에 연결된 상태지만 뷰는 어떤 오프젝트가 will, should, did를 실행하고 있는지 모른다.
+ closure방식으로 델리게이트 처리할 수 있음
    * 프로토콜이 처리하게 하느냐고 많은 비용이 들 수 있는데 클로져가 있으면, 클로져의 인자가 무엇인지 알고 있고 무엇을 반환할지 알고 있기 때문에 사실상 프로토콜을 정하는것과 동일하다
    * ScrollView를 예를 들면 스크롤이 끝나면 이 클로져를 실행해라 라는 의미 -> 클로저에게 처리를 맡기는 것
+ 클로져와 프로토콜 둘다 사용가능하지만 서로 완전히 대체가능하지는 않다.
+ 프로토콜은 이 오브젝트가 무엇을 위임할 수 있는지를 매우 분명히 할때 좋다.
+ 클로져는 에러 콜백(Error Callback), Multi-Thread 환경 어떤 처리가 오래 걸리다가 나중에 완료되면 끝났다고 알려줄때 좋다
+ Example
    * UIScrollView
    * weak var delegate: UIScrollViewDelegate?
    * @objc protocol UIScrollViewDelegate{
        optional func ~~
        optional func ~~
    }

### ImageView
+ URL에서 이미지 가져오는 방법
    * let url = imageURL
    * let imageData = NSData(contentOf: url as URL)
    * UIImage image = UIImage(data: imageData as Data)
+ UIImageView set
    * image {
        set {
            imageView.image = newValue
            imageView.sizeToFit()
            scrollView?.contentSize = imageView.frame
        }
    }

### Mulithreading
+ 멀티 쓰레딩이란, 일을 처리하는 별도의 쓰레드를 갖추는 것이다.
+ 싱글코어프로세서에서도 시분할 방식으로 문맥교환을 통해 여러 쓰레드를 작동시킨다
+ IOS에서 멀티 쓰레딩은 queue와 같다
+ 이 큐는 IOS 함수들을 포함하고 있다 (대부분 여기에 들어간 함수는 클로져로 되어 있다)
+ 큐는 여러개가 존재할 수 있고 스시템은 각각의 큐에서 꺼내서 각각의 쓰레드에서 동작시킨다
+ 시리얼큐(serial)는 큐에 있는 첫 번째 테스크가 끝나면 그 다음 테스크는 꺼내는 방식의 큐이다.
+ 병렬큐(concurrent)는 큐에서 테크를 꺼내 처리하는 동안 놀고있는 다른 쓰레드에서 다음 것들을 바로 처리하는 방식
+ Main Queue
    * 가장 중요한 큐 (very special serial queue)
    * 메인 큐는 모든 UI가 작동해야 할 곳에서 사용된다.
    * 이와 반대로 시간이나 리소스를 잡아먹는 UI외의 모든 처리는 메인큐 밖에서 처리해야만 한다.
    * 메인 큐에서 동작하는 것들은 직렬로 처리된다.
    * UI가 순서대로 예상가능하게 표현되어야 하기 떄문인다.
    * 메인 큐가 클로져나 함수를 꺼내 작업을 처리하는 유일한 떄는 메인큐가 한가할 때이다.
+ Other Queue
    * UI가 아닌 것들을 처리하는데 사용하는 큐

+ 큐에 뭔가를 집어넣는 방법
    * dispatch_async(queue) {
        /* do what you want to do here */ <- 클로저임 
    }
    * 2개의 arguments를 받음
        - queue
        - func(closure)
+ The Main Queue
    * main queue call
        - dispatch_get_main_queue() 함수 사용 -> swift 3.0 미만
        - DispatchQueue.main.async
+ The Other Queue
    * 다른 큐를 사용하는 방법은 시스템이 제공하는 병렬 큐들을 사용
    * 시스템이 제공하는 4가지 큐
    * 4개의 큐는 각자 맡고 있는 서비스(Quality Of Service)가 있다.
    * QOS는 시스템이 얼마나 특정 서비스에 중점을 두느냐를 말한다 -> 우선순위로 이해해도 된다.
    * 4가지 QOS
        - USER_INTERACTIVE: 가장 우선순위가 높은 큐 메인큐는 아니지만 즉각 처리가 필요한 부분
        - USER_INITIATED: 유저가 처리를 요청했지만 상호작용이 필요한 처리는 아님 시간은 조금 걸리지만 바로 처리해야함
        - UTILITY: 뒤에서 오랫동안 작동하는 작업 데이터를 가져오거나 데이터 베이스를 비운다던지 하는 경우
        - BACKGROUND: 오늘 해도 되고 내일 해도 되는 작업
    * other queue call
        - dispatch_get_global_queue(<one of the QOS>, 0) // 0 is a "reserved for future" 언젠가를 위해 남겨둔다는 의미로 항상 0으로 세팅
        - DispatchQueue.global.async
+ User Create Queue
    * custome queue call
        - dispatch_queue_create("name", DISPATCH_QUEUE_SERIAL)
        - DispatchQueue(label:"queuename")
    * 메인 큐 까지는 아니지만 높은 우선순위의 직렬큐로 생성된다.
+ GCD(Grand Central Dispatch)
    * 따로 공부해라
+ 추상적인 API
    * NSOpertaionQueue and NSOperation
    * 서로 다른 쓰레드에서 동작하는 2개의 객체가 서로 의존성이 있을때 사용
+ IOS API관점에서 멀티 쓰레딩
    * IOS 전반에는 쓰레드를 사용해서 비동기적으로 처리하는 수많은 메소드가 있다
    * 메소들의 인자중 하나인 클로저를 살펴보면 된다.
    * 클로저는 비동기으로 메인 큐 바깥에서 처리될 것
    * 대표적인 예 URLSession

### UITextField
+ UITextField는 UILabel과 같지만 텍스트를 편집할 수 있다.
+ UITextField가 "first responder"가 되면 키보드가 나타난다.
+ 키보드를 숨기고 싶으면 resignFirstResponder를 사용하면 된다.
+ Delegate 주로 return키와 함께 사용된다.
+ 키보드를 설정하려면 UITextField를 통하면 된다.
+ 키보드위에 커스텀 뷰 올릴때 inputAccessoryView