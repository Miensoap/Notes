#### multi-threading
- CPU 사용률 향상
- 응답성 향상
- 작업이 분리되어 코드가 간결
- 자원을 효율적으로 사용가능

### 쓰레드의 구현과 실행
- Thread 클래스를 상속
- Runnable 인터페이스 구현
```java
	class MyThread implements Runnable{
		public void run(){/*작업내용*/}
	}
```
##### Start()
- call stack을 생성 후 run()을 호출.

### 쓰레드의 우선순위
