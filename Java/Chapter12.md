# Chapter 12
## java.base 모듈
>참고 문헌 : 이것이 자바다

### 12.2 java.base 모듈
* 자바의 모든 모듈이 의존하는 기본 모듈로, 모듈 중 유일하게 requires하지 않아도 사용할 수 있다. 

  | 패키지       | 용도                                                |
  |-----------|---------------------------------------------------|
  | java.lang | 자바 언어의 기본 클래스를 제공                                 |
  | java.util | 자료 구조와 관련된 컬렉션 클래스를 제공                            |
  | java.text | **날짜 및 숫자** 를 원하는 형태의 **문자열** 로 만들어 주는 포맷 클래스를 제공 |
  | java.time | 날짜 및 시간을 조작하거나 연산하는 클래스를 제공                       |
  | java.io   | **입출력** 스트림 클래스를 제공                               |
  | java.net  | 네트워크 통신과 관련된 클래스를 제공                              |
  | java.nio  | 데이터 저장을 위한 Buffer 및 새로운 입출력 클래스 제공                |

#### java.lang
* 자바 언어의 기본적인 클래스를 담고 있는 패키지

  | 클래스                                                     | 용도                                                           |
  |---------------------------------------------------------|--------------------------------------------------------------|
  | object                                                  | 자바 클래스의 최상위 클래스로 사용                                          |
  | System                                                  | 키보드로부터 데이터를 입력받을 때, 콘솔로 출력, 프로세스 종료, 진행 시간 읽을 때, 시스템 속을 읽을 때 |
  | String                                                  | 문자열을 **저장하고 조작**                                             |
  | StringBuilder                                           | 효율적인 문자열 조작 기능이 필요할때                                         |
  | java.util.StringTokenizer                               | **구분자로** 연결된 문자열을 분리할 때                                      |
  | Byte, Short, Character, Integer, Float, Double, Boolean | 기본 타입의 값을 포장할 때 사용<br/>문자열을 기본 타입으로 변환할 때 사용                 |
  | Math                                                    | 수학계산이 필요할 때                                                  |
|  Class                                                   | 클래스의 메타 정보 등을 조사할 때                                          |

### 12.3 Object 클래스
* extends를 쓰지 않아도 암시적으로 상속되는 클래스.
1. boolean equal(Object obj) : 객체의 번지 비교하고 결과 리턴
    * `public boolean equals(Object obj)` 
    * 자동 타입 변환에 의해 모든 객체가 매개값 가능
    * 비교 연산자 `==`과 같은 결과 리턴
    * 재정의하여 동등 비교용으로 사용한다.
    * 동등 비교 : 객체가 달라도 내부의 데이터가 같은지 비교
    * Object 재정의 예시) `obj instanceof Member target`로 obg가 Member 타입인지 검사, 타입 변환 후 target 변수에 대입
2. int hashCode() : 객체의 해시코드를 리턴
    * `public int hashCode()`
    * 객체 해시코드는 객체를 식별하기 위한 정수
    * 객체의 메모리 번지를 이용하여 해시코드를 생성하기 때문에 객체마다 다른 정수값을 리턴한다.
    * 두 객체가 동등한지 비교한다. 
    * 객체의 데이터를 기준으로 재정의하여 새로운 정수값을 리턴하도록 한다.
    * 먼저 hashCode()로 리턴하는 정수값이 같은지 확인하고 equals()로 true 리턴하면 동등 객체
    * hashCode()를 재정의하지 않으면, hashSet에 같은 데이터의 학생 객체를 저장하면 객체가 다르기 때문에 따로 저장된다.
3. String toString() : 객체 문자 정보를 리턴
    * 객체의 문자 정보 : 객체를 문자열로 표현한 값
      * `클래스명@16진수해시코드`로 구성된 문자열을 리턴
      * `System.out.println() 메소드`는 기본 타입(byte, short, int, long, float, double, boolean)이거나 문자열이면, 해당값을 그대로 출력
    * #### 레코드
      * 데이터 전달을 위한 DTO를 작성할 때 반복적으로 사용되는 코드르 줄이기 위해 Java14부터 레코드가 도입.
      * `class` 대신 `record`를 사용하여 레코드 소스를 컴파일 하면 변수 타입과 이름을 이용하여 `private final` 필드가 자동 생성 되고 `생성자` 및 `Getter 메소드`가 자동으로 추가된다.
      * hasCode(), equals(), toString() 메소드를 `재정의`한 코드 자동 추가
    * #### 롬복
      * 자동 코드 생성 라이브러리
      * DTO 클래스 작성 시 Getter, Setter, haseCode(), equals(), toString() 메소드를 자동 생성
      * 차이점은 **필드가 final이 아니고**, 값을 읽는 Getter()는 **get000**로 Setter()는 **set000**로 생성
      * @Data가 붙게 되면 컴파일 과정에서 기본 생성자와 함께 Getter, Setter, haseCode(), equals(), toString()가 생성
        * | 어노테이션                    | 설명                                                                          |
          |--------------------------|-----------------------------------------------------------------------------|
        * | @NoArgsConstructer       | 기본 생성자 포함                                                                   |
        * | @AllArgsConstructor      | 모든 필들르 초기화하는 생성자 포함                                                         |
        * | @RequiredArgsConstructor | 기본적으로 매개변수가 없는 생성자 포함, 만약 final 또는 @NotNull이 붙은 필드가 있다면 이 필드만 초기화시키는 생성자 포함 |
        * | @Getter                  | Getter 메소드 포함                                                                        |
        * | @Setter                  | Setter 메소드 포함                                                               |
        * | @EqualsAndHashCode       | equals()와 hasCode() 메소드 포함                                                  |
        * | @ToString                | toString()메소드 포함                                                            |
        * final과 notnull의 차이점은 초기화된 final 필드는 변경할 수 없지만(Setter가 만들어지지 않음), @NotNull은 null이 아닌 다른 값으로 Setter를 통해 변경할 수 있다는 것이다.
### 12.4 System 클래스
* System 클래스를 통해 운영체제의 일부 기능을 이용 가능
  * | 정적멤버 | 이름                  | 용도                         |
    |------|---------------------|----------------------------|
    | 필드   | out                 | 콘솔에 문자 출력                  |
    | 필드   | err                 | 콘솔에 에러내용 출력                |
    | 필드   | in                  | 키보드 입력                     |
    | 메소드  | exit(int status)    | 프로세스 종료                    |
    | 메소드  | currentTiemMillis() | 현재 시간을 밀리초 단위의 long 값으로 리턴 |
    | 메소드  | nanoTime()          | 현재 시간을 나노초 단위의 long 값으로 리턴 |
    | 메소드  | getProperty()       | 운영체제와 사용자 정보 제공            |
    | 메소드  | getenv()            | 운영체제의 환경 변수 정보 제공          |
  
    * #### 콘솔 출력
    * `out 필드`로 콘솔에 원하는 문자열 출력
    * err과의 차이는 콘솔 종류에 따라 에러 내용이 빨간색으로 출력된다.
    * #### 키보드 입력
    * 자바는 키보드로 부터 입력된 키를 읽기 위해 System 클래스에서 `in 필드`를 제공
    * in 필드를 이용해 read() 메소드를 호출하면 입력된 키의 코드값을 얻을 수 있음
    * read() 메소드는 호출과 동시에 키 코드를 읽는 것이 아니라 `Enter`키를 누르기 전까지는 대기 상태. 키 입력 시 하나씩 읽는다.
    * `IOException`을 발생할 수 있는 코드이므로 예외 처리가 필요하다.
    * #### 프로세스 종료
    * 운영체제는 실행중인 프로그램을 `프로세스`로 관리한다.
    * 자바 프로그램을 시작하면 JVM 프로세스가 생성되고 이 프로세스가 main()메소드를 호출한다.
    * 프로세스 강제 종료 시 System.exit()메소스 사용
    * `System.exit(int status)`
    * int 매개값은` 종료 상태값`이라고 한다. 정상 종료는 0 , 비정상종료는 1 또는 -1로 주는 것이 관례
    * #### 진행 시간 읽기
    * 1970년 1월 1일 0시부터 시작해서 현재까지 진행된 시간을 리턴
    * 프로그램 처리 시간을 측정하는데 주로 사용, 프로그램 처리 시작시 한 번, 끝날 때 한 번 읽어 그 차이를 프로그램 처리 시간
    * #### 시스템 프로퍼티 읽기
    * 자바 프로그램이 시작될 때 자동 설정되는 시스템의 속성
    * java.sepcification.version : 자바 스펙버전
    * java.home : JDK 디렉토리 경로
    * os.name : 운영체제
    * user.name : 사용자 이름
    * user.home : 사용자 홈 디렉토리 경로
    * user.dir : 현재 디렉토리 경로

### 12.5 문자열 클래스
* #### String 클래스
* 문자열을 저장하고 조작할 때 사용
* byte 배열을 묹자열로 반환하는 경우
* `Stirng str = new String(byte[] bytes);` -> 기본 문자셋으로 byte 배열을 디코딩해서 String 객체로 생성
* `String str = new String(byte[] bytes, Stirng charsetName);` -> 특정 문자셋으로 byte 배열을 디코딩해서 String 객체로 생성
* #### StringBuilder 클래스
* String은 내부 문자열을 수정할 수 없다. 문자열을 결합하면 결합한 결과는 새로운 String 객체를 생성하는 것이다."
* 문자열의 + 연산은 새로운 String 객체가 생성되고 이전 객체는 계속 버리기 때문에 효율성이 나쁘다.
* 잦은 문자열 변경 작업 시, StringBuilder를 사용하는 것이 좋다.
* StringBuilder는 내부 버퍼에 문자열을 저장해두고 그안에서 추가, 수정, 삭제 작업을 한다.
* | 메소드                                     | 설명             |
  |-----------------------------------------|----------------|
  |StringBuilder.append(기본값/문자열)                         | 문자열 끝에 추가      |
  | StringBuilder.insert(위치, 기본값/문자열)                    | 문자열을 지정 위치에 추가 |
  | StringBuilder.delete(시작위치, 끝위치)                      | 문자열 일부를 삭제     |
  | StringBuilder.replace(시작 위치, 끝 위치, 문자열) | 문자열 일부를 대체     |
  | String.toString()                       | 완성된문자열을 리턴     |
* StringBuilder의 메소드들은 StringBuilder를 다시 리턴하기 때문에 연이어서 다른 메소드를 호출할 수 있는 `메소드 체이닝 패턴`을 사용할 수 있다.
* 메소드 체이닝 예시
```
String data = new StringBuilder()
        .append("DEF")
        .insert(0, "ABC")
        .delete(3,4)
        .toString();
```

* #### StringTokeizer 클래스
* 문자열이 구분자로 연결되어 있을 때, 구분자 기준 문자열 분리 시, String의 `split()`메소드 이용하거나 java.util 패키지의 StringTokenizer 클래스를 이용할 수 있다.
* 여러 종류가 아닌 **한 종류의 구분자**만 있을 때 StringTokenizer 사용 가능, 객체 생성시 첫번째 매개갑승로 전체 문자열을 주고, 두번째 매개값으로 구분자를 준다. 구분자 생략 시 공백으로 구분.
```
    String data = "홍길동/이수홍/박연수";
    StringTokenizer st = new StringTokenizer(data, "/");
    
```
* StringTokenizer 객체가 생성되면 분리된 문자열을 얻을 수 있다.
  * | 리턴타입    | 메소드             | 설명                |
    |---------|-----------------|-------------------|
    | int     | countTokens()   | 분리할 수 있는 문자열의 총 수 |   
    | boolean | hasMoreTokens() | 남아있는 문자열이 있는지 여부  |
    | String  | nextToken()     | 문자열을 하나씩 가져옴      |
    * `nextToken()` 메소드는 더 이상 불러올 문자열이 없다면 **예외를 발생**시킨다. `hasMoreTokens()` 메소드로 먼저 가져올 문자열이 있는지 먼저 조사하는 것이 좋다.
    ```java
    import java.util.StringTokenizer;
    public class StringTokenizerExample{
        public static void main(String[] args){
        String data1 = "홍길동,이수홍&박연수";
        String[] arr = data1.split(",&");
        for (String token :arr){
            System.out.println(token);
    }
    System.out.println();
    String data2 = "홍길동/이수홍/박연수";
    StringTokenizer st = new StringTokenizer(data2, "/");
    while (st.hasMoreTokens()){
        String token = st.nextToken();
        System.out.println(token);
    
            }
        }
    }
    ```
    
### 12.6 포장 클래스
* 자바는 기본 타입의 값을 갖는 객체를 새성할 수 있다. 이런 객체를 `포장객체`라고 한다. 값을 포장한다는 의미~
* | 기본 타입   | 포장클래스          |
  |---------|----------------|
  | byte    | java.lang.Byte |
  | char    | java.lang.Character      |
  | short   | java.lang.Short          |
  | int     | java.lang.Integer        |
  | long    | java.lang.Long           |
  | float   | java.lang.Float          |
  | double  | java.lang.Double         |
  | boolean | java.lang.Boolean        |
* 박싱 : 기본 타입의 값을 포장 객체로 만드는 과정
* 언박싱 : 포장 객체에서 기보 타입의 값을 얻어내는 과정을 언박싱
* 포장 객체는 포장하고 있는 **기본 타입의 값을 변경할 수 없고** 단지 객체 생성하는 데 목적이 있다. `컬렉션 객체` 때문에 필요!
* `Integer obj = 100; // 박싱`
* `int value = obj; //언박싱`
* 포장 객체는 내부 값을 비교하는 ==과 != 연산자를 사용할 수 없다. 두 연산자는 포장 객체의 번지를 비교하기 때문이다. 
* 하지만 boolean, char, byte,short int는 특정 범위의 값을 가지면 객체를 공유할 수 있다.
* equals()메소드로 내부의 값을 비교할 수 있다.

### 12.7 수학 클래스
* 수학 계산에 사용할 수 있는 메소드를 제공한다. 모두 정적 메소드이므로, 클래스로 바로 사용이 가능하다.
* | 구분   | 코드                                                               | 리턴값                                   |
  |------|------------------------------------------------------------------|---------------------------------------|
  | 절대값  | int v1 = Math.abs(-5);<br/> double v2 = Math.abs(-3.14);         | v1 =5<br/> v2=3.14                    |
  | 올림값  | double v3 = Math.ceil(5,3);<br/> double v4 = Math.ceil(-5.3);    | v3 =6.0<br/> v4 = -5.0                |
  | 버림값  | doubl v5 = Math.floor(5.3);<br/>   double v6 = Math.floor(-5.3); | v5 = 5.0<br/> v6 = -6.0               |
  | 최소값  | int v7 = Math.min(5.9);<br/>double v8 = Math.min(5.3,2.5)        | v7=5<br/>v8= -2.5                     |
  | 최대값  | int v9 = Math.max(5.9);<br/>double v10 = Math.max(5.3,2.5)       | v9=5<br/>v1= -2.5    v7 =9<br/>v8 =5.3 |
  | 랜덤값  | double v11 = Math.randon();                                      | 0.0<=v11<1.0                          |
  | 반올림값 | long v14 = Math.round(5.3);<br/> longv15 = Math.round(5.7);      | v14 = 5<br/> v15 = 6                  |
* `random()` 메소는 **0.0~1.0 사이의 난수**를 리턴한다. `n개의 정수`(start<=...<(start+n) 중 하나의 정수를 얻기 위해선 아래 공식을 사용한다.
`int num = (int) (Math.random() * n)+ start;`
* #### java.uil.Random
* boolean, int, double 난수를 얻을 수 있다.
* | 객체 생성             | 설명                     |
  |-------------------|------------------------|
  | Random()          | 현재 시간을 이용해서 종자값을 자동 설정 |
  | Random(long seed) | 주어진 종자값을 사용한다.         |
* 종자값 : 난수를 만드는 알고리즘에 사용되는 값으로 , 종자값이 같으면 같은 난수를 얻는다.
* nextBoolean(), nextDouble(), nextInt(), nextInt(int n)->0~n 중 하나의 int 타입 난수 리턴

### 12.8 날짜와 시간 클래스
* 컴퓨터의 날짜 및 시각을 읽을 수 있도록 java.uil 패키지에서 Date와 Calendar 클래스를 제공.
* 조작 가능하도록 java.time 패키지에서 LocalDateTime 등의 클래스 제공
#### Date
`Date date = new Date();`
* 현재 날짜를 문자열로 얻고 싶을 때, toString()메소드 사용
* 원하는 문자열로 얻고 싶을 땐, SimpleDateFormat클래스를 사용한다.
#### Calendar
`Calendar now = Calendar.getInstance();`
* Calendar 클래스의 정적 메소드 `getInstance()` 메소드를 통해 컴퓨터에 설정된 시간대를 기준으로 하위 객체를 얻을 수 있다.
* Calendar가 제공하는 날짜와 시간에 대한 정보를 얻기 위해 `get()` 메소드를 사용한다. 매개값으로 Calendar에 정의된 상수를 주면 상수가 의미하는 값 리턴
`int year = now.get(Calendar.YEAR); // 년도 리턴`
* Timezone 객체로 다른 시간ㄴ대의 Calendar를 얻을 수 있다.
* ```
  TimeZone timeZone = TimeZone.getInstance("America/Los_Angeles");
  Calendar now = Calendar.getInstance("timeZone);
  ```
#### 날짜와 시간 조작
* java.time.LocalDateTime 클래스로 날짜와 시간 조작
* plusYears(long), minusMonth(long)...

```
LocalDateTime now = LocalDateTime.now();
```
* DateTimeFormatter는 날짜와 시간을 주어진 문자열 패턴으로 변환할 때 사용한다. format()메소드 호출 시 매개값으로 제공하면 같은 패턴으로 문자열을 얻을 수 있다.
#### 날짜와 시간 비교
* isAfter(other), isBefore(other), is Equal(other) -> boolean으로 리턴
* until(other, unit) -> long으로 리턴, 주어진 단위 차이를 리턴
* 비교를 위해 특정 날짜와 시간으로 LocalDateTime 객체를 얻을 때 매개값을 모두 int 타입으로 제공한다.
`LocalDateTime target = LocalDateTime.of(year, month, dayOfMonth, hour, minute, second);`


### 12.9 형식 클래스
* 숫자 또는 날짜를 원하는 형태의 문자열로 변환해준다.
* java.text 패키지에 포함되어 있다.
* | Format 클래스       | 설명               |
  |------------------|------------------|
  | DecimalFormat    | 숫자를 형식화된 문자열로 변환 |
  | SimpleDateFormat | 날짜를 형식화된 문자열로 변환 |

### 12.10 정규 표현식 클래스
* 문자열이 정해져 있는 형식으로 구성되어있는지 검증 -> 이메일 형식 등
* 정규 표현식을 이용해 문자열이 올바르게 구성되어 있는지 검증한다.
* 정규 표현식 : 문자 또는 숫자와 관련된 표현과 반복 기호가 결합된 문자열이다.
* \.은 문자로서의 점(.)이고 .은 모든 문자 중에서 한 개의 문자를 뜻한다.
* \\는 역슬래시(\)을 의미한다.
#### Pattern 클래스 검증
* java.util.regex 패키지의 Pattern 클래스는 정규 표현식으로 문자열을 검증하는 matches() 메소드를 제공, 첫번째 매개값은 정규 표현식, 두번째 매개값은 검증할 문자열이다.
`boolean rsult = Pattern.matches("정규식", "검증할 문자열");`


### 12.11 리플렉션
* 자바는 클래스와 인터페이스의 메타 정보를 class 객체로 관리한다.
* 메타 정보 : 패키지 정보, 타입 정보, 멤버 정보
* 리플렉션 : 프로그램에서 메타 정보를 읽고 수정하는 행위
* 프로그램에서 Class 객체 얻는 방법

```
 Class clazz = 클래스.Class;   //클래스로부터 얻는 방법
 Class clazz = Class.forName("패키지... 클래스이름"); //클래스로부터 얻는 방법
 Class clazz = 객체참조변수.getClass(); //객체로부터 얻는 방법
 
```

#### 패키지와 타입 정보 얻기
* Package getPackage() : 패키지 정보 읽기
* String getSimpleName() : 패키지를 제외한 타입 이름
* String getName() : 패키지를 포함한 전체 타입 이름
* Constructor[] getDeclaredConstructor() : 생성자 정보 읽기
* Field[] geDeclaredFields() : 필드 정보 읽기
* Method[] getDeclaredMethods() : 메소드 정보 읽기
* Constructor, Field ,Method 모두 java.lang.reflect 패키지에 있고 각각 생성자, 필드, 메소드에 대한 선언부 정보를 제공한다.
#### 리소스 경로 얻기
* Class 객체는 클래스 파일의 경로 정보를 가지고 있기 때문에, 경로를 기존으로 상대 경로에 있는 다른 리소스 파일(이미지, XML, Property 파일)의 정보를 얻을 수 있다.
* URL getResource(Stirng name) : 리소스 파일의 URL 리턴
* InputStream getResourceAsStream(String name) : 리소스 파일의 InputStream 리턴
* ```
  String photoPath= clazz.getResource("phto1.jpg").getPath();
  ```
* 구현 객체에 재정의된 메소드 실행 내용이 다 다르기 때문에 어떤 객체가 매개값으로 들어오냐에 따라 결과가 다르게 나타난다.`(매개변수의 다형성)`
### 12.12 어노테이션 `@`
* 어노테이션 : 클래스 또는 인터페이스를 컴파일하거나 실행할 때 어덯게 처리해야 할 것인지 알려주는 설정 정보.
* 1. 컴파일 시 사용하는 정보 전달
* 2. 빌드 툴이 코드를 자동으로 생성할 때 사용하는 정보 전달
* 3. 실행 시 특정 기능을 처리할 때 사용하는 정보 전달
#### 어노테이션 타입 정의와 적용
* 어노테이션을 사용하기 위해서는 정의를 해야한다.
`public @interface AnnotationName{}`
* ` @AnnotationName` 으로 어노테이션을 사용한다.
* 어노테이션은 속성(타입, 이름)을 가질 수 있다.
* 기본값은 default 키워드로 지정할 수 있다.
* ```
    public @interface AnnotationName{
    String prop1();
    int prop2() default 1;

    }
  ```
* `@AnnotationName(prop1 = "값");// prop2는 기본값이 있기 때문에 생략 가능`
* 기본 속성인 value를 가질 수 있다.
* ```
    public @interface AnnotationName{
    String value();
    int prop2() default 1;

    }
  ```
* `@AnnotationName("값");`
* 다른 속성과 값을 같이 사용하고 싶다면 value를 명시해야 한다.
* `@AnnotationName(value="값", prop2=3);`

#### 어노테이션 적용 대상
* 어떤 대상에 설정 정보를 적용할 것인지 명시해야 한다.
* | ElementType 열거 상수 | 적용요소             |
  |-------------------|------------------|
  | TYPE              | 클래스, 인터페이스, 열거타입 |
  | ANNOTATION_TYPE   | 어노테이션            |
  | FIELD             | 필드               |
  | CONSTRUCTOR       | 생성자              |
  | METHOD            | 메소드              |
  | LOCAL_VARIABLE    | 로컬 변수            |
  | PACKAGE           | 패키지              |
* 적용 대상을 지정할 때 @Target 어노테이션을 사용한다.
* @Target의 기본 속성인 value는 ElementType 배열을 값으로 가진다.
* **적용 대상**을 **복수 개**로 지정하기 위해서
* ```
  @Target({ElementType.TYPE, ElementType.FIELD, ElementType.METHOD}) // 클래스, 필드, 메소드에 적용 가능, 생성자 적용 불가
    public @interface AnnotationName{
    }
  ``` 

#### 어노테이션 유지 정책
* 어노테이션을 얼마나 유지 할것인지 정해야 한다.
*  | RetentionalPolicy 열거 상수 | 적용 시점         | 제거 시점      |
   |-------------------------|---------------|------------|
   | SOURCE                  | 컴파일할 때 적용     | 컴파일 후      |
   | CLASS                   | 메모리로 로딩할 때 적용 | 메모리로 로딩된 후 |
   | RUNTIME                 | 실행할 때 적용      | 계속 유지      |
*   ```
    @Target({ElementType.TYPE, ElementType.FIELD, ElementType.METHOD}) // 클래스, 필드, 메소드에 적용 가능, 생성자 적용 불가
    @Rentention(RetentionPolicy.RUNTIME)
    public @interface AnnotationName{
    }
  ``` 
