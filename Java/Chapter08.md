# Chapter 08
## 인터페이스
>참고 문헌 : 이것이 자바다

### 8.1 인터페이스 역할
* 인터페이스 : 두 객체를 연결하는 접속기
* 인터페이스를 통해 간접 호출을 하여 인터페이스 뒤의 다른 객체가 실행된다.

### 8.2 인터페이스와 구현 클래스 선언
#### 인터페이스 선언
```
    interface 인터페이스명{ }
    
    public interface 인터페이스명{
    // 인터페이스가 가지는 멤버
        public 상수 필드
         public 추상 메소드
          public 디폴드 메소드
           public 정적 메소드
            public 메소드
             public 정적 메소드
             
    }
  
```
* 추상 메소드란 선언부만 있고 실행부인 중괄호가 없는 메소드

#### 구현 클래스 선언
1. 객체 A가 인터페이스의 추상 메소드를 호출하면
2. 인터페이스는 객체 B의 메소드를 실행한다.
__객체 B는 인터페이스에 선언된 추상 메소드와 동일한 선언부를 가진 메소드를 가지고 있어야 한다!__

* 객체 B를 인터페이스를 구현한(implement) 객체라고 한다.

`public class B implements 인터페이스명 {}`
* 
#### 변수 선언과 구현 객체 대입
* 인터페이스도 변수의 타입으로 사용할 수 있다.
* 인터페이스는 참조 타입에 속한다.(객체 참조 하지 않는다 == null)
```
    인터페이스명 in;
    인터페이스명 in = null;
```
* 인터페이스를 통해 구현 객체를 사용하려면, 인터페이스 변수에 구현 객체를 대입해야 한다. 구현 객체의 번지를 대입하는 것이다.
* 
```
in = new 객체B();
```
* 인터페이스 변수에 구현 객체가 대입이 되어야 변수를 통해 인터페이스의 추상 메소드를 호출할 수 있다. 이때 실행되는 것은 객체B의 메소드이다.

```
in.인터페이스의 추상메소드();
```

### 8.3 상수 필드

* 인터페이스는 public static final 특성의 `상수 필드`를 멤버로 가질 수 있다.
* 인터페이스에 선언된 필든느 모두 public static final 특성을 가지기 때문에 생략가능하다.
* 상수는 대문자로 작성하고 다른 단어로 구성되어 있으면 언더바로 연결

### 8.4 추상 메소드
* 인터페이스는 구현 클래스가 **재정의**해야 하는 public `추상 메소드`를 멤버로 가진다.
* 추상 메소드는 **리턴 타입, 메소드명, 매개변수**만 기술되고 중괄호를 붙이지 않는 메소드이다.
* 구현 클래스에서 추상 메소드를 재정의할때 인터페이스의 추상메소드는 기본적으로 public 접근 제한을 가지기 때문에 더 낮은 접근 제한으로 재정의할 수 없다.


### 8.5 디폴드 메소드
* 인터페이스는 완전한 실행 코드를 가진 `디폴트 메소드`를 선언할 수 있다.
* 디폴트 메소드는 실행부가 있다. 리턴타입 앞에 `default` 키워드를 붙인다.

`public default 리턴타입 메소드명(매개변수, ..){...}`
* 디폴트 메소드는 구현 객체가 필요하기 때문에 추상 메소드를 구현한 객체를 인터페이스 변수에 대입해야 한다.
* 구현 클래스는 디폴트 메소드를 재정의해서 자신에게 맞게 수정할 수 있다. 재정의 시, public 접근 제한자를 붙이고, default 키워드를 생략해야 한다.

### 8.6 정적 메소드

* `정적 메소드`는 구현 객체가 없어도 인터페이스명으로 접근하여 호출이 가능하다.
`public static 리터타입 메소드명(매개변수, ) {..}`

* 정적 메소드의 실행부 작성시, 상수 필드를 제외한 **추상 메소드, 디폴트 메소드, private 메소드 등을 호출할 수 없다!**
-> `구현 객체가 필요한 인스턴스 메소드이기 때문`


### 8.7 private 메소드
* 인터페이스에 외부에서 접근할 수 없는 `private 메소드`는 구현 객체가 필요한 메소드이다.
* private 메소드는 디폴트 메소드 안에서만 호출이 가능하지만, private 정적 메소드는 디폴트 메소드뿐만 아니라 정적 메소드 안에서도 호출이 가능하다.
* **디폴트와 정적 메소드들의 중복 코드를 줄이기 위함이다.**

### 8.8 다중 인터페이스 구현
* 구현 객체는 여러 개의 인터페이스를 implements할 수 있다.
* 구현 객체가 인터페이스A와 인터페이스B를 구현하고 있다면 각각의 인터페이스를 통해 구현 객체를 사용할 수 있다.

```
public class 구현 클래스명 implements 인터페이스A, 인터페이스B{

// 모든 인터페이스가 가진 추상 메소드를 재정의해야 한다.

}
```
* 두 인터페이스를 구현한 객체는 두 인터페이스 타입의 변수에 각각 대입될 수 있다.
```
 인터페이스A 변수 = new 구현 클래스명();
 인터페이스B 변수 = new 구현 클래스명();
```

### 8.9 인터페이스 상속
* 인터페이스는 **다른 인터페이스를 상속**할 수 있다.
* 클래스와 달리 `다중 상속`이 가능하다!
```
public interface 자식인터페이스 extends 부모인터페이스1, 부모인터페이스2{....}
```
* 자식 인터페이스의 구현 클래스는 자식 인터페이스의 메소드 뿐만 아니라 **부모 인터페이스의 모든 추상 메소드를 재정의**해야 한다.
* 구현 객체는 자식 및 부모 인터페이스 변수에 대입될 수 있다.
```
 자식 인터페이스 변수 = new 구현 클래스명();
 부모 인터페이스A 변수 = new 구현 클래스명();
 부모 인터페이스B 변수 = new 구현 클래스명();
```
* 구현 객체가 자식 인터페이스 변수에 대입되면 자식과 부모 인터페이스의 추상 메소드 모두 호출 가능
* 구현 객체가 부모 인터페이스 변수에 대입되면 부모 인터페이스에 선언된 추상 메소드만 호출 가능

### 8.10 타입 변환
* 인터페이스의 타입 변환은 인터페이스와 구현 클래스 간에 발생
* 인터페이스 변수 ->구현 객체를 대입하면 구현 객체는 인터페이스로 **자동 타입 변환**
* 인터페이스 타입 -> 구현 클래스 타입으로 변환 **(강제 타입 변환)**
#### 강제 타입 변환
* `캐스팅 기호(캐스팅할 구현 클래스명)`를 사용하여 인터페이스 타입 -> 구현 클래스 타입으로 변환


### 8.11 다형성
* 필드 타입으로 인터페이스를 선언하면 필드값으로 구현 객체를 대입할 수 있다.
```
 public class Car{
    Tire tire1 = new HanKookTire();
    Tire tire2 = new kumhoTire();
 }
```
* Car 객체 생성후 다른 구현 객체를 대입할 수도 있다.
```
Car myCar = new Car();
myCar.tire1 = new KumhoTire(); // 다른 객체 대입
```

#### 매개변수의 다형성
* 메소드 호출 시 매개값을 다양하기 위해 상속에서 매개변수 타입을 부모 타입으로 선언하고 호출 시 다양한 자식 객체를 대입했다.
* 매개 변수 타입을 인터페이스로 선언하면 메소드 호출 시 다양한 구현 객체를 대입할 수 있다.
* 인터페이스의 구현 객체를 매개값으로 줄 수 있다. 
* 구현 객체에 재정의된 메소드 실행 내용이 다 다르기 때문에 어떤 객체가 매개값으로 들어오냐에 따라 결과가 다르게 나타난다.`(매개변수의 다형성)`
### 8.12 객체 타입 확인
* 인터페이스에서 객체 타입을 확인하기 위해 `instanceof 연산자`를 사용한다.
* 메소드의 매개변수가 인터페이스 타입이면 메소드 호출 시 매개값은 해당 인터페이스를 구현하는 모든 객체가 될 수 있다.
* 만약 매개값이 특정 구현 객체일 경우에만 강제 타입 변환을 하고 싶다면 `instanceof 연산자` 사용하여 매개값의 타입을 검사한다.
```
    public void method(Vehicle vehicle){
    if(vehicle instanceof Bus){
        Bus bus = (Bus) vehicle;
        }
        }
```
* **Java 12**부터는 강제 타입 변환 없이 우측 타입 변수를 사용할 수 있다.

### 8.13 봉인된 인터페이스
* Java 15부터 `sealed` 인터페이스 사용