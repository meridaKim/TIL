# Chapter 02
## 변수와 타입
>참고 문헌 : 이것이 자바다

### 2.1 변수 선언

데이터를 어디에, 어떤 방식으로 저장할지 정해져 있지 않다면 메모리 관리가 무척 어려워진다.

#### 변수 : 하나의 값을 저장할 수 있는 메모리 번지에 붙여진 이름 
#### 변수 선언 : 어떤 타입의 데이터를 저장할 것이니지 변수 이름이 무엇인지를 결정한다.
#### 변수에 값 저장 : 우측 값을 좌측 변수에 대입한다. 이 때 대입 연산자인 = 을 사용한다.

* 변수 초기화 : 변수에 최초로 값을 대입하는 행위, 이때의 값을 초기값이라 한다.
```
int x = 10; // 변수 x에 10 대입
int y = x; // 변수 y에 x 값 대입
```

### 2.2 정수 타입
| 값의 분류 | 기본 타입                                                           |
|-------|-----------------------------------------------------------------|
| 정수    | int(4byte), long(8byte), short(2byte), char(2byte), byte(1byte) |
| 실수    | float, double                                                   |
| 논리    | boolean                                                         |

#### 메모리 사용 크기 순(부호 있는 정수 타입)
|종류|byte|short|int|long|
|-------------|--------|-----|----|-----|
|메모리 사용 크기 (bit)|8|16|32|64|

#### 리터럴 : 코드에서 프로그래머가 직접 입력한 값

* 2진수 : 0b, OB로 시작
```
int x = 0b1011;
int y = 0B10100;
```

* 8진수 : 0으로 시작하고 0~7 숫자로 작성

* 10진수 : 소수점이 없는 0~9 숫자로 작성

* 16진수 : 0x 또는 0X로 시작하고 0~9 숫자 또는 A,B,C,D,E,F 또는 a,b,c,d,e,f로 작성

* 변수에 허용 범위를 초과한 값을 대입하면 __컴파일 오류 발생__

* long 타입은 "l(L)"을 붙여 컴파일러에게 알린다.


### 2.3 문자 타입(char)

* 하나의 문자를 작은 따옴표(')로 감산 것을 문자 리터럴이라고 한다.
*  유니코드로 변환되어 저장된다. 
`A -> 65(10진수),0x0041(16진수) / 가 -> 44032`
* 문자 타입 초기화 : 공백문자(유니코드 : 32)를 포함해서 초기화한다
`char c = ' ';`

### 실수 타입 : 부동 소수점 방식으로 메모리에 저장
| 타입      | 메모리 크기                                         | 유효 소수 이하 자리 |
|---------|------------------------------------------------|------------|
| float   | 4byte / 32bit(1bit[부호비트]+8bit[지수]+23bit[가수])   | 7자리        |
| double  | 8byte / 64bit (1bit[부호비트]+11bit[지수]+52bit[가수]) | 8자리        |

* double 타입은 float 타입보다 약 2배의 유효 자릿수를 가지기 때문에 보다 정확한 데이터 저장이 가능하다.

### 2.5 논리 타입
`boolean 타입 : true/false`

### 2.6 문자열 타입
* 여러 개의 문자들을 ""(큰 따옴표)로 감싸면 문자열
* 문자열은 __String__ 타입을 사용하여 저장한다.
#### 이스케이프 문자 : 역슬래쉬가 붙은 문자

| 이스케이프 문자 |                       |
|----------|-----------------------|
| \"       | " 문자 포함               |
| \'       | ' 문자 포함               |
| \\       | \ 문자 포함               |
| \u16진수   | 16진수 유니코드에 해당하는 문자 포함 |
| \t       | 출력 시 탭만큼 띄움           |
| \n       | 출력 시 줄바꿈              |
| \r       | 출력 시 캐리지 리턴           |


### 2.7 자동 타입 변환
* 허용 범위가 작은 타입이 허용 범위가 큰 타입으로 대입될 때 발생

`byte < short, char < int < long < float < double`

* char -> int
```
char charVaule = 'A'
int intValue = charValue; // 65 저장
```

* 예외 : char 타입보다 허용 범위가 작은 byte 타입은 char 타입으로 자동 변환될 수 없다. 
char는 음수 포함하지 않지만 byte은 __음수 포함!__

### 2.8 강제 타입 변환
* 큰 허용 범위 타입을 작은 허용 범위 타입으로 __쪼개어서 저장__
* int -> byte 
* long-> int 
* int-> char 
* 실수(float, double) -> 정수(byte, short, int, long)

### 2.9 연산식에서 자동 타입 변환
```
byte x = 10;
byte y = 20;
byte result = x+y; //컴파일 에러 발생
int result = x+y ;
```

```
int intValue = 10;
double doubleValue = 5.5;
double result = intValue+doubleValue; //intValue가 double로 자동 변환
```
```
int intValue = 10;
double doubleValue = 5.5;
int result = intValue+(int)doubleValue; //int타입 연산이 필요하면 강제 변환
```
```
int x = 1;
int y = 2;
double result = x/y; //결과는 0.0

/*
x와 y 중에 하나, 또는 둘다 double 타입으로 변경해야 결과가 0.5
*/
```
* +연산자는 문자열끼리 합치기
```
int intValue = 3+7; -> 10
String str = "3"+7; ->37
String str = 3+"7"; ->37
String str = 1 +(2+3); -> 15
String str = 1 +"2" + 3;  -> 123
String str = 1 + 2 +"3"; -> 33
String str = "1" + (2+3); -> 중괄호에 의해 덧셈 연산 우선 수행
```

### 2.10 문자열을 기본 타입으로 변환
| 변환 타입             | 사용 예                    |
|-------------------|-------------------------|
| String -> byte    | Byte.parseByte();       |
| String -> short   | Short.parseShort();     |
| String -> int     | Integer.parseInt();     |
| String -> long    | Long.parseLong();       |
| String -> float   | Float.parseFloat();     |
| String -> double  | Double.parseDouble();   |
| String -> boolean | Boolean.parseBoolean(); |

### 2. 12 콘솔로 변수값 출력
| 메소드             | 의미                         |
|-----------------|----------------------------|
| println()       | 괄호 안의 내용을 출력하고 __행간을 바꿔라__ |
| print()         | 괄호 안의 내용을 출력하고 행간 바꾸지 말아라  |
| printf("%d", a) | 형식 문자열에 맞추어 뒤의 값을 출력해라     |

#### 형식화된 문자열
* 정수 : %d
* 실수 : %f
* 문자열 : %s
* 특수 문자:  \t, \n

### 2.13 키보드 입력 데이터를 변수에 저장

`Scanner scan = new Scanner(System.in);`
`String input = scan. nextLine(); // Enter키 누르면 입력된 문자열을 읽고 변수 input에 저장`

* 자바의 기본타입(byte, short, int, long, float,doulbe, boolean) 동일한지 비교할 때는 "==" 사용
* String 동일한지 비교할 때는 equals()를 사용한다.