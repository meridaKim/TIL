# Chapter 13
## 제네릭
>참고 문헌 : 이것이 자바다

### 13.1 제네릭이란?
* 객체가 어떤 내용물이 저장되는지 알 수 없을 때 Object의 content 필드를 선언하는 것은 좋지 않다.
* 클래스 생성시 저장할 필드가 무엇인지 타입을 미리 알려주면 클래스는 필드에 무엇이 대입되고 읽을 때 어떤 타입으로 제공할 지 알게된다.
* 제네릭 : 결정되지 않은 타입을 파라미터로 처리하고 실제 사용할 때 파라미터를 구체적인 타입으로 대체시키는 기능
* ```
    public class Box<T> {
        public T content;
  }
    ```
* Box 클래스에서 결정되지 않은 content 타입을 T라는 타입 파라미터로 정의한 것
* <T> : T가 타입 파라미터를 의미한다.
* ```
    Box<String> box = new Box<String>();
  box.content = "안녕";
  String content = box.content; //강제 타입 변환없이 안녕을 얻을 수 있음
  ```
* 타입 파라미터를 대체하는 타입은 클래스, 인터페이스이다. int가 아닌 Integer로 파라미터 타입 지정하는 이유
* 변수 선언할 때와 동일한 타입으로 호출한다면 생성자 호출 시 생성자에는 타입을 명시하지 않고 <>만 붙일 수 있다.
  `Box<String> box = new Box<String>;`-> `Box<String> box = new Box<>();`

### 13.2 제네릭 타입
* 제네릭 타입 : 결정되지 않은 타입을 파라미터로 가지는 클래스와 인터페이스
* 일반적으로 타입 파라미터는 대문자 알파벳 한 글자로 표현
* ```
  public class 클래스명<A,B...>{...}
  public interface 인터페이스명<A,B>{..}
    ```
### 13.3 제네릭 메소드
* 제네릭 메소드는 타입 파라미터를 가지고 있는 메소드
* 제네릭 타입과 차이점 : 타입 파라미터가 메소드 선언부에 정의된다.
* 리턴 타입 앞에 <> 기호를 추가하고 타입 파라미터를 정의한뒤, 리턴 타입과 매개변수 타입에서 사용
* ```
  public <A,B...> 리턴타입 메소드명(매개변수, ...){...}
    ```
* boxting() 메소드는 타입 파라미터로 <T>를 정의하고, 매개 변수 타입과 리턴타입에서 T를 사용한다.
* ```
  public <T> Box<T> boxing(T t){...}
    ```
* 타입 파라미터는 매개값이 어떤 타입이냐에 따라 컴파일 과정에서 구체적인 타입으로 대체된다.
* ```
  Box<Integer> box1 =  boxing(100);
    ```
### 13.4 제한된 타입 파라미터
* 숫자를 연산하는 제네릭 메서드는 대체 타입으로 Number 또는 자식 클래스(Byte, Short, Integer, Long, Double)로 제한할 필요가 있다.
* 제한된 타입 파라미터 : 특정 타입과 자식 또는 구현 관계에 있는 타입만 대체할 수 있는 타입 파라미터
* `public <T extends 상위타입> 리턴 타입 메소드(매개변수,...){...}`
* 상위 타입은 인터페이스도 가능. implements를 사용하지 않는다.
* ```
  public <T extends Number> boolean compare(T t1, T t2){
    double v1 = t1.doubleValue(); //Number의 doubleValue()메소드 사용
    double v2 = t2.doubleValue();
    return (v1 == v2);
    
  }
    ``` 
### 13.5 와일드카드 타입 파라미터
* 제네릭 타입을 매개값이나 리턴 타입으로 사용할 때 타입 파라미터로 `?`와일드카드를 사용할 수 있다.
* ? : 범위에 있는 모든 타입으로 대체 가능
* 타입 파라미터의 대체 타입으로 Student와 자식 클래스인 HighStudent,MiddleStudent만 가능하도록 매개 변수 선언
* `리턴타입 메소드명(제너릭 타입<? extends Student> 변수){...}`
* 반대로 Worker와 부모 클래스인 person만 가능하도록 매개변수를 선언
* `리턴타입 메소드명(제너릭 타입<? super Worker> 변수){...}`
* 어떤 타입이든 가능하도록 선언
* `리턴타입 메소드명(제너릭 타입<?> 변수){...}`