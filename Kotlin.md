## 코틀린 문법
### 변수
  * 모든 변수는 객체다
    - 기본적인 primitive 타입도 클래스로 취급한다!
    
  * Mutable 지원
    - var -> 변수 val -> 상수
    
  * 늦은 초기화(lazy init) 지원
    - lateinit 키워드 붙이기
    - primitive 타입에는 적용이 불가능 하다
    - by lazy {} 꼴로 lazy초기화하는 클래스를 정의 가능
    
### 기본 타입/컬렉션 지원(Pair, Range, List..etc)
  

  * **Pair**
    - (변수 A, 변수 B...)같은 데이터 클래스 형으로 Pair 지원
      ```kotlin
      fun main()
      {
       var A = Pair("sss",3)
       assert(A == Pair("sss",3))
       
       var (a,b) = Pair("sss",3)
       assert(a.equals("sss"))
       assert(b.equals(3))
      }
      ```
    - HashMap, TreeMap에서 사용 가능
    - "key" to "value" 형태로 사용 가능하다
    
  * **Range**(Rust랑 거의 비슷함)
    - A~B까지 -> A..B꼴로 for문에서 유용하게 사용 가능
      ```kotlin
      fun main(){
       val arr = arrayOf(0,1,2,3,4)
       /* arr = {0,1,2,3,4} */
       for(i in 0..4)
       {
        assert(arr[i] == i)
        /*assert(arr[0] == 0)*/
        /*assert(arr[1] == 1)*/
        /*assert(arr[2] == 2)*/
        /* .....etc.........*/
       }
      }
      ```
    - 변수/상수 in "구간" 꼴로 범위 안에 있는지 확인 가능 
      ```kotlin
      fun main(){ 
         assert(6 in 0..9)
      }
      ```
      
  * **Any**
    - 모든 타입(클래스)의 어머니격인 타입(클래스)
    - when문에서 타입을 유연하게 쓰도록 활용 가능
      ```kotlin
      fun main(){
         var data: Any = 10
         when(data){
          is String ->println("data is String Type!")
          20, 30 ->println("data is 20 or 30")
          in 1..10 ->println("data is in 1..10!")
          else ->println("data is Not Valid Type!")
         }
      }
      ```
  * **Unit**
    - c언어의 void 형과 비슷하다
    - 함수형 프로그래밍할 때 void 생기면 곤란한 상황을 대처한다
      ```kotlin
      fun some(): Unit{
       println(10 + 20)
      }
      fun main()
      {
       assert(some() == Unit)
      }
      ```  
  * **Null-Safty Type**
    - ?연산자를 지원한다!
    - 
  
### OOP
  * 생성자
    - 주 생성자 + 멤버 선언 동시에
      ```kotlin
         class User(var name: String){
         }
      ```
    - 주 생성자 -> init 블럭에서 초기화
      ```kotlin
         class User(_name: String){
          var name: String
          init
          {
           this.name = _name
          }
         }
      ```
    - 주 생성자 생략 + 보조 생성자(constructor()) 사용 
      ```kotlin
         class User{
          var name: String
          constructor(_name: String)
          {
           this.name = _name
          }
         }
      ```
    - 주 생성자 + 보조 생성자(constructor()) 연쇄 호출 적용
      (자바,코틀린은 기본적으로 오버로딩이 없어서 유용하다) 
      (단, 초기화가 아니라 Re-Assign이 되므로 var타입으로 정의해서 초기값을 넣어야 한다)
      ```kotlin
       class User(name: String){
       
        var count: Int = 0 //Initialize가 아니라 Re-Assign이므로 무조건 variable타입
        val name: String = name
        var email: String = "aaaa@gmail.com" //Initialize가 아니라 Re-Assign이므로 무조건 variable타입
        
        constructor(name: String, count: Int)
        : this(name) {
         this.count = count
        }
        
        constructor(name:String, count: Int, email: String)
        : this(name, count) {
        this.email = email
        }
       }
      ```
  * 상속 
    - 변수 혹은 값(상수) 앞에 open 키워드로 상속될 동작(함수)을 표현
      ```kotlin
      open class Vehicle(open var name: String){
       open val maxPassengerCount: Int = 0 
      }
      class Plane(override var name: String) : Vehicle(name){
       override val maxPassengerCount: Int = 20
      }
      fun main()
      {
       var IncheonBusanLine: Vehicle = Plane("747") //Java 베이스이므로, 다형성이 기본임
       assert(IncheonBusanLine.maxPassengerCount == 20)
      }
      ```
    - 상속 받는 함수는 override 키워드 사용
    - 상속 받은 함수에 대해 오버로딩 X 무조건 가상함수로 작성(언어 레벨에섬 막힘)
    
  * 접근 제한자: 
    - public : 모든 파일(기본적으로 getter setter를 만드는 public이 기본 타입이다)
    - internal : 같은 파일
    - protected : 사용 불가
    - private : 파일 내부에서 이용 가능

  * Data Class
    - equals()비교시 객체의 참조 그 자체(주소값)이 아니라 데이터를 비교한다!
    
  * 컴파일러 자동 생성 멤버 함수
    - equals() : 즉시 초기화된 내부 데이터 객체 를 비교한다(lateinit 변수는 비교하지 않는다)!
    - toString() : 즉시 초기화된 내부 데이터 객체를 String으로 포매팅한다(lateinit 변수는 비교하지 않는다)!
      

