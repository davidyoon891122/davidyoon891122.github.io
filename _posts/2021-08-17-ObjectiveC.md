### Objective C
1. 변수
+ int, long, float, double, char
+ formatter
    * int -> %d
    * long -> %ld
    * float -> %f
    * double -> %f
    * *char -> %s
+ NSInteger: 현재 사용하고 있는 아키텍처에 맞게 사이즈가 자동으로 설정되는 애플의 Foundation 프레임워크에 있는 특별한 primitive data type
    * primitive type이며 32bit에서 NSInteger, NSUInteger는 int, unsigned int에 mapping된다.
    * 64bit에서는 NSInteger, NSUInteger는 long, unsigned long에 mapping 된다.
    * NSInteger nsInt = 100;
    * 출력: NSlog(@"result : %i", nsInt); long일 경우 %li
+ CGFloat: Foundation 프레임워크에 있는 primitive data type float, double에 자동 맵핑
    * CoreGraphics 
    * CGFloat cgFloat = 10.3;
    * 출력: NSLog(@"result : %f", cgFloat);
+ BOOL: boolean type
    * BOOL isTrue = YES; -> YES 는 1
    * BOOL isFalse = NO; -> NO 는 0


2. 조건문
+ if (// condition) {
    // statement
}else if (// condition) {
    // statement
}else 


3. 함수
+ 함수 선언
    * (returnType)functionName:(parameterType) parameterName
                    withAnotherValue:(secondParamterType) secondParameterName
        {
            // statement    
        }
    * (void)addIntegers:(NSInteger) firstValue
                    withAnotherValue: (NSInteger) secondValue
        {
            NSLog(@"result: %i", firstValue + secondValue);
    }
+ 함수호출
    * [self addIntegers:5 withAnotherValue: 10]; -> 15 출력
    
3. NSString
+ NSString 은 스트링형태를 다루는 ObjectiveC 객체
+ 객체 생성
    * NSString *myName = [[NSString alloc] initWithFormat:@"David Yoon"];
    * 출력: NSLog(@"result: %@", myName); -> 객체 포멧은 %@
    * NSString *otherName = [NSString stringWithFormat:@"your name"];
+ 문자열 출력
    * NSLog(@"%i", [myName length]);
+ 문자열 복사
    * NSStirng *tmp = [NSString stringWithString:myName];
+ 문자열 합치기
    * NSString *tmp = [str1 stringByAppendingString:str2];
+ 문자열 합치기 2
    * NSMutableString *str1 = @"This is"
    * NSString *str2 = @"Love"
    * [str1 appendString:str2];
+ 문자열 비교
    * NSString *tmp = str1;
    * if ([str1 isEqualToString:tmp] == YES)



4. NSNumber
+ Foundation 프레임워크의 NSNumber 클래스 인스턴스를 생성하는 것 -> 자바의 wrapper 클래스 개념
+ 객체를 만드는 데 다른 객체를 사용하는 몇몇의 Cocoa 클래스들이 있기 때문(primitive type 사용 불가)
+ 생성
    * NSNumber *appleNumber = [[NSNumber alloc] initWithInt:5];
    * NSNumber *carNumber = [NSNumber numberWithInt: 3295];
+ NSNumber to CGFloat
    * CGFloat cgFloat = [carNumber floatValue];
+ NSInteger to NSNumber 
    * NSInteger originInteger = 50;
    * NSNumber *numberForOrigin = [NSNumber numberWithInteger: originInteger];

5. LifeCycle
+ 주기
    * 앱실행 -> main() -> AppDelegate -> ViewController
+ 앱 구성요소 보기
    * UIKit: UI를 그리는 다양한 컴포넌트를 가지고 있는 라이브러리

+ 앱 생명주기
    * 앱실행 -> 인액티브 -> 액티브 -> 백그라운드 -> 서스팬드 -> 스톱

5. UIView
+ UIViewController
    * 큰 장면 덩어리를 관리 
    * UIViewController를 만들면 자동적으로 하나의 UIView가 따라온다.
+ 화면에 보이는 것들의 기본속성
    * 사각형이 기본
    * 사각형을 그리기 위한 위치, 크기 필요
    * (x,y), width, height -> frame
    * 색깔(Color)
+ IOS 좌표계
    * 왼쪽 위에서 부터 (0,0) 시작 -> 처음 constrains 없이 뷰 넣으면 왼쪽 상단에 몰려있음
+ UIView 생성
    * CGRect testRect = CGRectMake(0,0,30,30);
    * UIView *testView = [[UIView alloc] initWithFrame: testRect];
+ 화면에 뷰 추가
    * addSubView
    * [부모뷰 addSubView: 자식뷰]
    * [self.view addSubView: testView];
+ 색추가
    * self.view.backgroundcolor = UIColor.redColor;
    * testView.backgroundcolor = [UIColor blueColor];

6. UIView_2
+ [parent addSubView child];
+ 화면에서 삭제하기
    * [child removeFromSuperview];
+ 부모뷰 뿐만 아니라 다른뷰에도 addSubView 가능
    * [secondView addSubView:thirdView];
    * 좌표가 0,0이면 secondView 왼쪽위에서 부터 그려짐 기준이 부모 왼쪽 위에 점으로 시작
+ 이동시키기
    * frame 에 들어가는 CGRect 좌표로 view 이동 가능
    * secondView.frame = CGRectMake(200,200,70,70); 으로 이동 가능
+ 화면 숨기기
    * hidden
    * thirdView.hidden = true;
+ 투명도
    * alpha
    * min: 0, max: 1.0
    * 투명도가 줄어드는 것이라 0이어도 메모리는 잡아먹음
    * 페이드효과 만들 때 사용
    * [UIView animationWithDuration:0.4 delay: 1.0f options:UIViewAnimationOptionCurveEaseIn animations:^{
        thirdView.alpha = 0.0f;
    } completion:^(BOOL finished) {
        
    }]

7. Self, Super
+ Self
    * 나 자신, 현재 메소드가 변수가 소속되어 있는 Class
    * ViewController.m 에서 self는 ViewController
    * Appdelegate.m 에서는 self = appDelegate
    * .h 파일에서 self사용할 일 없음
    * 다른언어에서는 this라고 불림

+ Super
    * 내 위에 무언가를 지칭한다
+ 상속
    * 그대로 물려받다. [inherit]
    * UIView 상속 받아 새로운 뷰 생성 가능
+ superclass
    * 내가 상속받은 class
    * NSObject(최상의 클래스) -> UIResponder -> UIViewController 
    * NSObject -> UIResponder -> Appdelegate
+ superview
    * self.view.superview 는 null 자동 생성 뷰이기 떄문에 슈퍼뷰 없음
    * testView.superview 는 UIView(self.view)
    * 뷰에 태그 붙이기 
        - self.view.tag = 20 (기본값은 0)

8. UILabel
+ text
    * 사용자에게 단순히 보여지는 text
        - 메뉴 가격 (static form)
    * 사용자가 입력할 수 있는 text
        - 글쓰기 form (input form)
    * 사용자의 행위에 따라 변하는 text
        - 장바구니 가격 form (dynamic form)
+ UILabel 은 static, dynamic에 적합
+ UILable 속성
    * 사격형
    * 텍스트
    * 배경색
    * font
        - testLabel.font = [UIFont systemFontOfSize:30];
    * textAlignment
        - testLabel.textAlignment = NSTextAlignmentCenter;

9. UIImageView
+ UIImage
    * 이미지 파일 데이터를 화면에 쉽게 출력할 수 있게 도와주는 도구
    * file -> data -> UIImage -> UIImageView -> 사용자
+ UIImageView 생성
    * UIImage *testImage = [UIImage imageNamed: @"imageName.png"];
    * UIImageView *testImageView = [[UIImageView alloc] initWithFrame: CGRectMake(0,0, 200,200);
    * testImageView.image = testImage;
    * testImageView.contentMode = UIViewContentModeScaleAspectFill -> 원본 비율에 맞게 크기 채워서 이미지 출려 옵션
    * testImageView.contentMode = UIViewContentModeScaleAspectFit -> 원본 비율에 맞게 프레임 사이즈에 맞게 이미지 출력 옵션
    * [self.view addSubView:testImageView];

+ 프레임 사이즈 출력
    * NSLog(@"%@", NSStringFromCGRect(testImageView));

+ 파일 경로 가져오기
    * NSString *path = [[UIBundle mainBundle] pathForResource:@"fileName", ofType:@"fileType"];
    * NSData *data = [NSData dataWithContentOfFile:path];
    * UIImage *imageWithData = [UIImage imageWithData: data];
    