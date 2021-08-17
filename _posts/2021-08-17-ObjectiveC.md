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