# Chapter 04
## 조건문과 반복
>참고 문헌 : 이것이 자바다

### 4.1 코드 실행 흐름 제어

제어문은 조건식과 중괄호 {} 블록으로 구성된다.
제어문은 __조건식__ 과 __반복문__ 두 종류를 가진다.
#### 조건식 : if, switch
#### 반복문 : for, while, do-while -> 제어문 처음으로 되돌아가는 것을 looping이라 한다.
* 변수 초기화 : 변수에 최초로 값을 대입하는 행위, 이때의 값을 초기값이라 한다.

### 4.2 if문
* if문
```
 if (조건식){
           -> //조건식이 true일 때 실행
 }
 -> 조건식이 false일 때 실행
```
* if-else 문
```
 if (조건식){
           -> //조건식이 true일 때 실행
 }
 else{
            -> 조건식이 false일 때 실행
 }
```
* else-if 문

```
if (조건식){
                    -> //조건식이 true일 때 실행
} else if( 조건식 2){
                    -> 조건식이 false이고 조건식2가 true이면 실행
}else{
                       -> 조건식, 조건식2가 모두 false이면 실행
}
```
* 중첩 if문 가능

### 4.3 switch문

* 뱐수의 값에 따라 실행문이 결정된다.
```
switch(조건식){
       case 값1 :            -> //변수가 값 1일 경우
        break;
       case 값2 :
        break;
       default:             -> //변수가 값1, 값2 모두 아닐 때(생략 가능)
       
}
```
* Java 12 이후부터 EXpressions(표현식) 사용 가능
```
switch(조건식){
       case 값1 -> System.out.println();
       case 값2 -> System.out.println();
       default -> System.out.println();
       
}
```

### 4.4 for문

* double 타입은 float 타입보다 약 2배의 유효 자릿수를 가지기 때문에 보다 정확한 데이터 저장이 가능하다.
```
for (1. 초기화식;, 2. 조건식;, 4.증감식){
    
    3. 실행문
}
```
* for문의 초기화식에서 선언된 변수는 블록 안 로컬 변수이므로, for 문 밖에서 사용하고 싶다면 for문 이전에 선언하자
* for문 작성 시 초기화식에서 float 타입 사용 금지(부동 소수점 금지)
* 중첩 for문 가능


### 4.5 while문

* 조건식이 true일 때 계속해서 반복, false면 while문 종료
* while(true)은 무한 반복이므로, while문 빠져나갈 코드도 함께 작성해주어야 한다.

### 4.6 do-while문

#### while vs do-while

* while문은 시작할 때부터 조건식을 평가하여 블록 내부를 실행할지 결정
* do-while문은 블록 내부를 먼저 실행하고, 실행 결과에 따라 반복 실행 계속할지 결정
```
do {
        1. 실행문
}while(2.조건식);   -> while()뒤 무조건 세미콜론!
```



### 4.7 break문

* 반복문인 for 문, while 문, do-while문을 실행 중지하거나 조건문인 switch문을 종료할 때 사용한다.

#### 중첩된 반복문에서의 break문
중첩된 반복문은 가장 가까운 반복문만 종료한다.
중첩된 반복문에서 바깥 반복문을 종료시키려면, 바깥쪽 반복문에 이름(레이블)을 붙이고, "break 이름;"을 사용하면 된다.

```
Label : for () {

    for(){
        break Label;
    }
}

```

### 4.8 continue문

* continue문은 for문, while문,do-while문에서만 사용
* continue문 실행되면 for문의 증감식, while문, do-while문의 조건식으로 바로 이동
* 반복문을 종료하지 않고 계속 반복