# Chapter 15
## 컬렉션 자료구조
>참고 문헌 : 이것이 자바다

### 15.1 컬렉션 프레임워크
* 자료 구조를 바탕으로 객체들을 효율적으로 추가, 삭제, 검색할 수 있도록 관련된 인터페이스와 클래스는 java.util 패키지에 포함

  | 인터페이스           | 특징                            | 구현 클래스                                  |
    |-----------------|-------------------------------|-----------------------------------------|
  | Collection.List | **순서를 유지**하고 저장, 중복 저장 가능     | ArrayList, Vector, LinkedList           |
  | Collection.Set  | 순서를 유지하지 않고 저장, **중복 저장 불가**  | HashSet, TreeSet                        |
  | Map             | **키와 값**으로 구성된 엔트리 저장, **키 중복 저장 불가** | HaspMap, Hashtable, TreeMap, Properties |


### 15.2 List
* 객체를 인텍스로 관리하기 때문에 객체를 저장하면 인덱스가 부여되고, 객체를 검색, 삭제가 가능하다.
* 객체 자체 저장이 아닌 객체의 번지를 저장한다.

  | 기능    | 메소드                           | 설명                      |
  |-------|-------------------------------|-------------------------|
  | 객체 추가 | boolean add(E e)              | 주어진 객체를 맨 끝에 추가         |
  | 객체 추가 | void add(int index E element) | 주어진 인덱스에 객체를 추가         |
  | 객체 추가 | set(int index, E element)     | 주어진 인덱스의 객체를 새로운 객체로 바꿈 |
  | 객체 검색 | boolean contains(Object o)    | 주어진 객체가 저장되어 있는지 여부     |
  | 객체 검색 | E get(int index)              | 주어진 인덱스에 저장된 객체를 리턴     |
  | 객체 검색 | isEmpty()                     | 컬렉션이 비어 있는지 조사          |
  | 객체 검색 | int size()                    | 저장되어 있는 전체 객체 수를 리턴     |
  | 객체 삭제 | void clear()                  | 저장된 모든 객체를 삭제           |
| | 객체 삭제 | E remove(int index)           | 주어진 인덱스에 저장된 객체를 삭제     |
| | 객체 삭제 | boolean remove(Object o)      | 주어진 객체를 삭제              |

#### ArrayList
* 일반 배열과의 차이점 : **제한 없이 객체 추가 가능**
* 동일한 객체를 중복 저장할 때, 동일한 번지가 저장된다.

#### Vector
* ArrayList와의 차이점 : 동기화된 메소드로 구성되어 있기 때문에 멀티 스레드가 동시에 Vector() 메소드 실행 불가.
* `멀티 스레드 환경`에서 안전하게 객체를 추가, 삭제 가능

#### Vector
* ArrayList와의 차이점 : 인접 객체를 체인처럼 연결해서 관리
* 특정 위치에서 객체를 삽입하거나 삭제하면 **바로 앞뒤 링크만 변경**하면 되므로 빈번한 객체 삭제와 사입이 일어나는 곳에서 ArrayList보다 좋은 성능 발휘

### 15.3 Set 
* 저장 순서가 유지 되지 않음
* 객체 중복 저장 불가
* 하나의 null만 저장

  | 기능  | 메소드                        | 설명                                        |
  |-----|----------------------------|-------------------------------------------|
  | 객체 추가 | boolean add(E e)           | 주어진 객체를 성공적으로 저장하면 true리턴, 중복 객체면 false 리턴 |
  | 객체 검색 | boolean contains(Object o) | 주어진 객체가 저장되어 있는지 여부                       |
  | 객체 검색 | Iterator<E> iterator()     | 저장된 객체를 한 번씩 가져오는 반복자 리턴                  |
  | 객체 검색 | isEmpty()                  | 컬렉션이 비어 있는지 조사                            |
  | 객체 검색 | int size()                 | 저장되어 있는 전체 객체 수를 리턴                       |
  | 객체 삭제 | void clear()               | 저장된 모든 객체를 삭제                             |
  | 객체 삭제 | boolean remove(Object o)   | 주어진 객체를 삭제                        |
* set 컬렉션은 인덱스로 객체 검색하여 가져오는 메소드가 없기 때문에 객체 반복해서 가져와야 한다.
* 1. for 문 이용
```
set<E> set = new HashSet<>();
for(E e:set){
    ...
}
```
* 2. iterator()메소드 이용
```
set<E> set = new HashSet<>();
Iterator<E> iterator = set.iterator();

```
| 리턴 타입   | 메소드       | 설명                             |
|---------|-----------|--------------------------------|
| boolean | hasNext() | 가져올 객체가 있으면 true, 없으면 false 리턴 |
| E       | next()    | 컬렉션에서 하나의 객체를 가져온다.            |
| void    | remove()  | next()로 가져온 객체를 Set 컬렉션에서 제거   |
```

while(iterator.hasNext()){
    E e = iterator.next();
}

```
#### HashSet
* 동일한 객체는 중복 저장하지 않는다. 다른 객체라도 hashCode() 메소드의 리턴값이 같고, equals() true리턴 시 동일 객체라 판단하여 저장하지 않는다.
* 문자열 저장할 경우, 같은 문자열을 갖는 String 객체는 동등한 객체로 간주한다.

### 15.4 Map 
* 키와 값으로 구성된 엔트리 객체를 저장
* `키와 값은 모두 객체`
* **키 중복 저장 가능, 값은 중복 저장 불가**
* 기존에 저장된 키와 동일한 키로 값을 저장하면 기존의 값은 없어지고 새로운 값으로 대체

  | 기능    | 메소드                               | 설명                                        |
  |-------|-----------------------------------|-------------------------------------------|
  | 객체 추가 | V put(K key, V value)             | 주어진 키와 값을 추가, 저장이 되면 값을 리턴                |
  | 객체 검색 | boolean containsKey(Object key)   | 주어진 키가 있는지 여부                             |
  | 객체 검색 | boolean containsKey(Object value) | 주어진 값이 있는지 여부                             |
  | 객체 검색 | Set<Map.entry<K,V>> entrySet()    | 키와 값의 쌍으로 구성된 모든 Map.Entry 객체 Set에 담아서 리턴 |
  | 객체 검색 | V get(Object key)                 | 주어진 키의 값을 리턴                              |
  | 객체 검색 | boolean isEmpty()                 | 컬렉션이 비어있는지 여부                             |
  | 객체 검색 | Set<K> keySet()                   | 모든 키를 Set 객체에 담아서 리턴                      |
  | 객체 검색 | int size()                        | 저장되어 있는 키의 총 수 리턴                         |
  | 객체 검색 | Collection<V> values()            | 저장된 모든 값 Collection에 담아서 리턴               |
  | 객체 삭제 | void clear()                      | 모든 키와 값을 삭제                               |
  | 객체 삭제 | V remove(Object key)              | 주어진 키와 일치하는 Map.Entry 삭제, 삭제가 되면 값을 리턴    |
#### HashMap
`Map<K,V> map = new HashMap<K,V>();`

#### Hashtable
* HashMap과의 차이점 : 동기화된 메소드로 구성되어 있기 때문에 멀티 스레드가 동시에 메소드를 실행할 수 없음

#### Properties
* Hashtable의 자식 클래스, Hashtable의 특징 가짐
* 키와 값을 String 타입으로 제한한 컬렉션
* 확장자가 .properties인 프로퍼티 파일을 읽을 때 사용
* load() 메소드로 프로퍼티 파일의 내용을 메모리로 로드
* 일반적으로 프로퍼티 파일은 클래스 파일과 함께 저장한다. 그렇기 때문에 클래스 파일을 기준으로 상대 경로를 이용하여 읽는 것이 편리
* Class 객체의 getResourceAsStream() 메소드는 주어진 상대 경로의 리소스 파일을 읽는 InputStream 리턴

```
    Properties properties = new Properties();
    properties.load();
```
### 15.5 검색 기능을 강화시킨 컬렉션

* #### Set.TreeSet
* 이진 트리 기반으로 한 Set 컬렉션
* 부모 노드의 객체와 비교하여 낮은 것은 왼쪽 자식 노드, 높은 것은 오른쪽 자식 노드에 저장
* byte 배열을 문자열로 반환하는 경우

* #### Map.TreeMap
* TreeSet과의 차이점은 키와 값이 저장된 Entry를 저장한다.
* 부모 노드의 객체와 비교하여 낮은 것은 왼쪽 자식 노드, 높은 것은 오른쪽 자식 노드에 저장

* #### Comparable과 Comparator
* TreeSet과 TreeMap에 저장되는 객체는 저장과 동시에 오름차순 정렬되는데, 객체가 Comparable 인터페이스를 구현하고 있어야 가능하다.
* Integer,Double, String타입 모두 Comparable 인터페이스 구현
* Comparable 인터페이스에는 compareTo()메소드가 정의되어 있다.

| 리턴 타입 | 메소드            | 설명                                    |
|-------|----------------|---------------------------------------|
| int   | compareTo(T o) | 주어진 객체와 같으면 0 리턴, 작으면 음수 리턴, 크면 양수 리턴 |
* 비교 기능이 없는 Comparable 비구현 객체를 저장하고 싶을 땐 TreeSet, TreeMap 생성할 때 비교자 제공
```
    TreeSet<E> treeSet = new TreeSet<E>(new ComparatorImpl());
    TreeMap<K,V> treeMap = new TreeMap<K,V>(new ComparatorImpl());
    
```
* Comparator 인터페이스에는 compare()메소드 정의되어 있다.

  | 리턴 타입 | 메소드                 | 설명                                                                  |
  |-------|---------------------|---------------------------------------------------------------------|
  | int   | compare(T o1, T o2) | o1과 o2 같으면 0 리턴, o1이 o2보다 앞에 오게하려면 음수 리턴, , o1이 o2보다 뒤에 오게하려면 양수 리턴 |


### 15.6 LIFO, FIFO 
* 후입 선출은 stack, 선입선출은 Queue
#### Stack
| 리턴 타입 | 메소드          | 설명               |
|-------|--------------|------------------|
| E     | push(E item) | 주어진 객체를 스택에 넣는다. |
| E     | pop()        | 스택의 맨 위 객체를 빼낸다. |
#### Queue
| 리턴 타입   | 메소드         | 설명              |
|---------|-------------|-----------------|
| boolean | offter(E e) | 주어진 객체를 큐에 넣는다. |
| E       | poll()      | 큐에서 객체를 빼낸다.    |




### 15.8 수정할 수 없는 컬렉션
* List, Set, Map 인터페잇의 정적 메소드인 of()로 생성
* List, Set, Map 인터페잇의 정적 메소드인 copyOf()로 생성
