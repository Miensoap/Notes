## Generics
- complie - time type check
- 다룰 객체의 타입을 미리 명시해서 타입 안정성 제공 / 타입체크와 형변환 생략
```java
	class Box(
		Object item;

		void setItem(Object item){ this.item = item;}
		Object getItem() { return item;}
	)

	class Box<T>{ //지네릭 타입 T선언
		T item;

		void setItem(T item){ this.item = item; }
		T getItem() { return item;}
	}

	// <T> : type , <E> : element, <K> : key
```
```java
	Box<String> b = new Box<String>(); // 타입 T대신 실제타입지정
	b.setItem(new Object()); // 에러. String 이외타입불가
	b.setItem("ABC"); 
	String item = b.getItem(); //형변환 생략가능
```
- 지네릭 클래스의 타입 지정 안할시 Object로 간주
	- unchecked or unsafe operation

- 지네릭클래스 = 원시타입(raw) + <타입변수>
- 인스턴스별로 다르게 동작이 가능
- static 멤버에는 타입변수 사용불가.
- 지네릭 타입 배열 생성 불가.
	- 컴파일 시점에 어떤 타입인지 new 연산자가 알 수 없음

---

### 지네릭 클래스의 객체

### 제한된 지네릭 클래스

### 와일드카드 '?'

### 지네릭 메서드

### 지네릭 타입의 형변환

#### 지네릭 타입의 제거

---

## 열거형(enums)
- 서로 관련된 상수를 편리하게 선언
```java
	class Card{
		enum Kind{CLOVER, HEART, DIAMOND, SPADE} //열거형 Kind정의
		enum Value{TWO,THREE,FOUR}

		final Kind kind;
		final Value valud;
	}
```
---

## 애너테이션(annotation)
- 소스코드 안에 다른 프로그램을 위한 정보를 미리 포함

- @Override : 오버라이딩
- @Deprecated : 앞으로 사용하지 않을 것을 권장 
- @SuppressWarnings  : 특정 경고메시지 억제
- @SafeVarargs : 지네릭스 타입의 가변인자
- @FunctionalInterface : 함수형인터페이스
- @Native : native메서드에서 참조되는 상수
- @Target* : 애너테이션 적용가능한 대상 지정
- @Documented* : 애너테이션 정보를 javadoc문서에 포함
- @Inherited* : 애너테이션이 자손클래스에 상속되도록함
- @REtention* : 애너테이션이 유지되는 범위 지정
- @Repeatable* : 애너테이션을 반복적용할수있게함

```java
	@interface 애너테이션이름{
		타입 요소이름(); // 애너테이션 요소 선언
	}
```



