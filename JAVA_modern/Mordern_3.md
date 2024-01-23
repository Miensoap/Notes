### 함수형 인터페이스
- 하나의 추상 메서드만을 정의하는 인터페이스
- 함수형 인터페이스를 기대하는 곳에 람다 표현식 사용가능
	- 람다 표현식을 이용해 메서드를 즉석으로 제공. 
	- 람다 표현식 전체가 함수형 인터페이스의 인스턴스로 취급.
```java
java.util.function 
Predicate<T>
Function<T>
Supplier<T>
Consumer<T>
Bina
```