# 코틀린 정리

## 변수
  * 모든 변수는 객체다
    - 기본적인 primitive 타입도 클래스로 취급한다!
    
  * Mutable 지원
    - var -> 변수 val -> 상수
    
  * 늦은 초기화(lazy init) 지원
    - lateinit 키워드 붙이기
    - primitive 타입에는 적용이 불가능 하다
    - by lazy {} 꼴로 lazy초기화하는 클래스를 정의 가능
    
## 기본 타입 지원(Tuple, Pair, Range)
  
  * **Tuple** 
    - (변수 A, 변수 B...)
      
  * **Pair**
    - (변수 A, 변수 B...)같은 클래스 형으로 Pair 지원
    - HashMap, TreeMap에서 사용 가능
    - "key" to "value" 형태로 사용 가능하다
      
  * **Range**(Rust랑 거의 비슷함)
    - to..from 꼴로 사용 가능
    - in "구간" 꼴로 범위 안에 있는지 확인 가능 ex.) assert(6 == in 0..9) 
      
  * **Any**
    - 모든 클래스가 상속 받는 클래스
    - 말 그대로 모든 타입을 대변한다
      
  * **Unit**
    - void 형과 비슷하다
    - 함수형 프로그래밍할 떄 void 생기면 곤란한 상황을 대처한다
      
  * **Null**
    - 아아
  
## OOP
  * 상속 
    - 변수 혹은 값(상수) 앞에 open 키워드로 상속될 동작(함수)을 표현
    - 상속 받는 함수는 override 키워드 사용
    - 상속 받은 함수에 대해 오버로딩 X 무조건 가상함수로 작성(언어 레벨에섬 막힘)
    
  * 접근 제한자: 
    - public : 모든 파일(기본적으로 getter setter를 만드는 public이 기본 타입이다)
    - internal : 같은 파일
    - protected : 사용 불가
    - private : 파일 내부에서 이용 가능

  * Data 전용 객체
    - C++ Struct랑 비슷한데 동작(함수) 정의할 수 없게 강제 되어있다
    
  * 컴파일러 자동 생성 멤버 함수
    - equals() : 즉시 초기화된 내부데이터 객체를 비교한다(lateinit 변수는 비교하지 않는다)!
    - toString() : 즉시 초기화된 내부데이터 객체를 String으로 포매팅한다(lateinit 변수는 비교하지 않는다)!
      
