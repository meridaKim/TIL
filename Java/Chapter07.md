# Chapter 07
## 상속
>참고 문헌 : 이것이 자바다

### 7.1 상속 개념

* `상속 : 부모가 자식에게 물려주는 행위`
* 부모 클래스의 필드와 메소드를 자식 클래스에게 물려줄 수 있다.
* 중복 코드를 줄여 개발 시간을 단축시킨다. 
* 클래스의 수정을 최소화 할 수 있다.

### 7.2 클래스 상속
* 프로그램에서는 자식이 부모를 선택한다.
* 자바에서는 다중 상속을 허용하지 않는다.

```
pubic class 자식 클래스 extends 부모 클래스{
}

```

### 7.3 부모 생성자 호출
* 부모 객체가 먼저 생성된 다음에 자식 객체가 생성된다.
* 자식 객체가 생성될 때 부모 객체가 먼저 생성된 후 자식 객체가 생성된다.
* `지식클래스 변수 = new 자식 클래스();`
* 모든 객체는 생성자를 호출해야만 생성된다. 부모 객체의 생성자도 호출되어야 하는데, 자식 생성자 내에 `super`에 의해 호출된다.
* super는 컴파일 과정에서 자식 클래스에 자동 추가된다. 만약 부모 클래스에 기본 생성자가 없다면 컴파일 에러 발생
```
     public 자식클래스() {
         super();
     }
```
* 부모 클래스에 기본 생성자가 없고 매개변수를 갖는 생성자만 있다면, 개발자는 super(매개값, )코드를 직접 넣어야 한다. 매개값의 타입과 개수가 일치하는 부모 생성자를 호출한다.
```
     public 자식클래스() {
         super(매개값,...);
     }
```

### 7.4 메소드 재정의
* `메소드 오버라이딩 :메소드가 자식 클래스에서 사용하기에 적합하지 않을 때, 자식 클래스에서 재정의하여 사용`
* `메소드 오버라이딩(어노테이션 @Override)`이 되면, 부모 메소드는 숨겨지고 자식 메소드가 우선적으로 사용된다.
#### 오버라이딩 주의사항
1. 부모 메소드의 선언부(리턴 타입, 메소드 이름, 매개변수)와 동일해야 한다.
2. 접근 제한을 더 강하게 오버라이딩할 수 없다.(public -> private 불가)
3. 새로운 예외를 throws 할 수 없다.
#### 부모 메소드 호출
* 자식 메소드가 부모의 일부 변경 내용을 제외하고는 그대로 가지고 있어야 한다.
* `super.method()`를 통해 공동 작업 처리 기법을 이용할 수 있다.
* 우선 처리가 되어야 할 내용을 먼저 작성하면 된다.

### 7.5 final 클래스와 final 메소드
* `final 클래스 : 더 이상 상속할 수 없는 클래스, 자식 클래스를 만들 수 없음`
* `final 메소드 : 부모 클래스를 상속해서 자식 클래스를 선언할 때, 부모 클래스에 선언된 final 메소드는 자식 클래스에서 재정의 불가`

### 7.6 protected 접근 제한자
* 상속과 관련된 접근 제한자로, public 과 default의 중간쯤애 해당하는 접근 제한을 한다.
* 같은 패키지에서는 default처럼 접근이 가능하지만 다른 패키지에서는 상속 받은 자식 클래스만 접근을 허용한다.
* 필드와 생성자 그리고 메소드 선언에 사용될 수 있다.


### 7.7 타입 변환
* `타입 변환: 타입을 다른 타입으로 변환`
* 클래스 타입 변환은 `상속 관계에 있는 클래스 사이`에서 발생한다.

#### 자동 타입 변환
* 자식이 부모의 특징과 기능을 상속받는 상황에서는 자동적으로 타입 변환이 일어난다.
* 자식 클래스에서 객체를 생성하고 이것을 부모 클래스 변수에 대입하면 자동 타입 변환이 일어난다.
* cat과 animal 변수는 타입만 다를 뿐, 같은 Cat 객체를 참조한다. `cat == aniaml ->true`

```
Cat cat = new Cat();
Animal animal = Cat();
Animal animal = new Cat();
```
* 부모 타입으로 자동 타입 변환된 이후에는 부모 클래스에 선언된 필드와 메소드만 접근이 가능하다.
* 변수는 자식 객체를 참조하지만 변수로 접근 간으한 멤버는 부모 클래스 멤버로 한정된다.
* 자식 클래스에서 오버라이딩된 메소드가 있다면 부모 메소드 대신 오버라이딩된 메소드가 호출된다.

```java
class Parent{
    void method1(){
        
    }
    void method2(){
        
    }
}
```
```java
class Child extends Parent{
    void method2(){
        
    }
    void method3(){
        
    }
}
```
```java
class ChildEx{
    public static void main(String[] args){
        Child child = new Child();
        Parent parent = child;
        
        parent.method1();
        parent.method2(); //child 오버라이딩된 메소드 호출
        parent.method3(); //호출 불가능
    }
}
```
#### 강제 타입 변환
* 캐스팅 연산자()를 통해 강제 타입 변환
* 자식 객체가 부모 타입으로 자동 변환된 후 다시 자식 타입으로 변환할 때 강제 타입 변환 사용 가능

```
    Parent parent = new Child();
    Child child = (Child) parent;
```
* 자식 타입에 선언된 필드와 메소드를 꼭 사용해야 한다면 강제 타입 변환을 해서 다시 자식 타입으로 변환해야 한다.
```java
class Parent{
    void method1(){
        
    }
    void method2(){
        
    }
}
```
```java
class Child extends Parent{
    String field2;
    void method3(){
        
    }
}
```
```java
class ChildEx{
    public static void main(String[] args){
        Parent parent = new Child();
        parent.method1();
        parent.field2 ="11"; //접근 불가능
        parent.method3(); //접근 불가능
        
        Child child = (Child) parent;
        child.field2 = "11"; //가능
        child.method3();    //가능
    }
}
```
### 7.8 다형성
* `다형성 : 사용방법은 동일하지만 실행결과가 다양하게 나오는 성질`
* 두 자식 클래스이 하나의 부모 클래스의 메소드를 오버라이딩을 하고 있다면 두 자식 클래스는 다르기 대문에 실행결과가 다르게 나온다.
* **자동 타입 변화 + 메소드 오버라이딩 = 다형성**

#### 필드 다형성
* `필드 다형성 : 필드 타입은 동일하지만 대입되는 객체가 달라져서 실행 결과가 다양하게 나오는 것`
```
    public class Car{
    public Tire tire;
    
    public void run(){
        tire.roll(); // tire 필드에 대입된 객체의 roll() 메소드 호출
    }
    }
```
```
    Car myCar = new Car(); // Car 객체 생성
    myCar.tire = new HanKookTire(); // HanKookTire객체 Tire 필드에 대입
    myCar.tire = new KumhoTire();  // KumhoTire객체 Tire 필드에 대입
    myCar.run(); // 대입된 타이어의 roll() 메소드 호출한다. 결과는 타이어에 따라 다름
```
#### 매개변수 다형성
* 메소드가 클래스 타입의 매개변수를 가지고 있을 경우, 호출할 때 동일한 타입의 객체를 제공하는 것이 정석이지만 자식 객체를 제공할 수 도 있다.
* 매개값으로 자식(탈것) 객체와 자식의 자식(버스, 택시) 객체도 제공할 수 있다.
* 어떤 자식(버스, 택시) 객체가 제공되는냐에 따라 부모(운전)의 실행 결과가 달라진다.

### 7.9 객체 타입 확인
* 변수가 참조하는 객체의 타입을 확인하고자 할 때, `instanceof` 연산자 사용
* `boolean result = 객체 instanceof 타입;`
* 객체가 우항의 타입이면 true, 아니면 false
* Child 타입으로 강제 타입 변환하기 전에 매개값이 Child 타입인지 여부 확인시 사용(Child 타입이 아니면 강제 타입 변환을 할 수 없기 때문)


### 7.10 추상 클래스
* `추상 : 실체 간의 공통되는 특성을 추출`
* `추상 클래스 : 클래스들의 공통적인 필드나 메소드를 추출해서 선언한 클래스`
* 추상 클래스는 실체 클래스의 __부모 역할__
* 실체 클래스는 추상 클래스를 상속해서 공통적인 필드나 메소드를 물려받을 수 있다.
* 추상 클래스는 `extends` 뒤에만 올 수 있다.
#### 추상 클래스 선언
* 클래스 선언에 `abstract` 키워드를 붙인다.
* 추상 클래스는 new 연산자를 이용해 객체를 직접 만들지 못하고 상속을 통해 자식 클래스만 만들 수 있다. 이때 추상클래스의 메소드를 호출할 수 있다.
* **필드, 메소드** 선언 가능
#### 추상 메소드와 재정의
* 추상 클래스의 메소드 선언부만 동일하고 자식 클래스의 실행 내용은 클래스마다 다르다.
* 추상 클래스는 추상 메소드를 선언할 수 있다.
* `abstract 리턴타입 메소드명(매개변수, );`
* 추상 메소드는 자식 클래스의 공통 메소드라는 것만 정의할 뿐, 실행 내용을 가지지 않는다.
```java
    public abstract class Animal{
    abstract void sound();
}
```
* 추상 메소드는 자식 클래스에서 **반드시 재정의**해서 실행 내용을 채워야 한다.
```java
public class AbstractmethodEx{
    public static void main(String[] args){
        Dog dog = new Dog();
        dog.sound();
        
        Cat cat = new Cat();
        cat.sound();
        
        animalSound(new Dog()); //animal로 자동 타입 변환
        animalSound(new Cat()); //animal로 자동 타입 변환
        animalSound
        public static void animalSound(Animal animal){
            animal.sound(); //재정의된 메소드 호출
        }
    }
}
```
### 7.11 봉인된 클래스
* Java 15부터 무분별한 자식 클래스 생성을 방지하기 위해 sealed 클래스 도입
* Permits 키워드 뒤에 상속 가능한 클래스를 지정해야 한다.
* `public sealed class Person permits Employee, Manager{}`
* 봉인된 클래스를 상속받는 클래스는 final 또는 non-sealed 키워드로 선언해야 한다.
```
    public fianl class Employee extends Person{} //자식 클래스 만들 수 없음
    public non-sealed class Manager extends Person{} // 자식 클래스를 만들 수 있음
```