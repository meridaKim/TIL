# Chapter 17
## 스트림 요소 처리
>참고 문헌 : 이것이 자바다

### 17.1 스트림이란?
* 컬렉션과 배열에 저장된 요소를 반복 처리 위해 `for문`과 `Iterator`를 이용 -> java8부터 Stream 지원
* 요소들이 하나씩 흘러가면서 처리된다는 의미를 가진다.
* forEach()메소드로 요소를 어떻게 처리할지 람다식 제공
```
    Stream<String> stream = list.stream();
    stream.forEach(item -> //아이템 처리);
```
* Iterator와의 차이점
* 1. 내부 반복자이므로 처리 속도가 빠르고 병렬 처리에 효율적이다.
* 2. 람다식으로 다양한 요소 처리를 정의할 수 있다.
* 3. 중간 처리와 최종 처리를 수행하도록 파이프라인을 형성할 수 있다.
### 17.2 내부 반복자
* `for문`과 `Iterator` 컬렉션 요소를 컬렉션 바깥쪽으로 반복해서 가져와 처리(`외부 반복자`)
* 스트림은 요소처리 방법을 컬렉션 내부로 주입시켜 요소를 반복 처리(`내부 반복자`)


### 17.3 중간 처리와 최종 처리
* 스트림은 하나 이상 연결될 수 있다.
* 컬렉션의 오리지널 스트림 뒤에 필터링 중간 스트림이 연결될 수 있고 그 뒤에 매핑 중간 스트림이 연결될 수 있다.
* 스트림끼리 연결되어 있는 것을 `스트림 파이프라인`
* 오리지널과 집계처리 사이의 중간 스트림
* 1. 최종 처리를 위해 필터링
* 2. 요소를 변환(매핑)
* 3. 최종 처리는 중간 처리에서 정제된 요소를 반복하거나 집계(카운팅, 총합, 평균) 작업 수행


```
    //Student 스트림
    Stream<Student> studentStream = list.stream();
    //score
    IntStream scoreStream = studentStream.mapToInt(student -> student.getScore() //Student 객체를 getScore()메소드의 리턴값으로 매핑);
    double avg = scoreStream.average().getAsDouble();
```
* 메소드 체이닝 패턴을 이용
```
    double avg = list.stream()
    .mapToInt(Student -> studnet.getScore())
    .average()
    .getAsDouble();
```

### 17.4 리소스로부터 스트림 얻기
* java.util.stream 패키지에는 BaseStream 인터페이스를 부모로 한 자식 인터페이스들이 있고 상속 관계를 가진다.
* Stream : 객체 요소를 처리하는 스트림
* IntStream, DoubleStream, LongStream : 기본 타입은 요소를 처리하는 스트림


### 17.5 요소 걸러내기(필터링)
* 요소를 걸러내는 중간 처리 기능
* distinct() : 중복 제거 -> string 경우, equals()리턴 값 true이면 동일한 요소로 판단
* filter() : 조건 필터링, 매개 타입은 요소 타입에 따른 함수형 인터페이스이므로 람다식으로 작성 가능 -> 매개값으로 주어진 predicate true 리턴 요소만 필터링

### 17.6 요소 변환(매핑)
* 스트림 요소를 다른 요소로 변환하는 중간 처리 기능.
* mapXxx() : 요소를 다른 요소로 변환한 새로운 스트림 리턴 -> 매개타입 Function을 가짐
* flatMapXxx() : 하나의 요소를 복수 개의 요소들로 변환한 새로운 스트림을 리턴


### 17.7 요소 정렬
* 요소를 오름차순 또는 내림차순으로 정렬
* Comparable 구현 객체의 정렬 : stream.sorted(Comparator.reverseOrder());
* Comparator를 이용한 정렬

### 17.8 요소를 하나씩 처리(루핑)
* 스트림에서 요소를 하나씩 반복해서 가져와 처리하는 것
* looping.peak() : 중간 처리 메소드, 최종처리가 뒤에 붙지 않으면 동작하지 않는다.
* looping.forEach() : 최종 처리 메소드

### 17.9 요소 조건 만족 여부(매칭)
* 요소들이 특정 조건에 만족하는지 여부를 조사하는 최종 처리 기능
* allMatch(), anyMatch(), noneMatch() : 매개값으로 주어진 Predicate가 리턴하는 값에 따라 true, false 리턴

### 17.10 요소 기본 집계
* 최종 처리 기능으로 요소들을 처리해서 카운팅, 합계, 평균값, 최대값, 최소값등 하나의 값으로 산출되는 것
* 대량의 데이터 가공 -> 하나의 값으로 축소 (리덕션)
* OptionalXXX : get(), getAsDouble(), getAsInt(), getAsLong()호출하면 최종값 얻을 수 있다.
* Optional.isPresent() : 집계값이 있는지 여부
* Optional.orElse() : 집계값이 없을 경우 디폴트 값 설정
* Optional.ifPresent(Consumer) : 집계값이 있을 경우 Consumer에서 처리

### 17.11 요소 커스텀 집계
* sum(), average(), count(), max(), min(), reduce()->스트림에 요소 없을 경우 예외 발생, identity 매개값 주어질 경우 디폴트 값으로 리턴

### 17.12 요소 수집
* Stream.collect(Collector<T,A,R> collector) : 필터링 또는 매핑된 요소들을 새로운 컬렉션에 수집하고 컬렉션 리턴
* T : 요소, A : 누적기 , R : 요소가 저장될 컬렉션
* groupingBy()메소드로 그룹핑 가능

### 17.13 요소 병렬 처리
* 멀티 코어 cpu 환경에서 전체 요소를 분할해서 각각의 코어가 병렬적으로 처리되는 것
