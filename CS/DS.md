# 자료구조
---

### ADT(abstract daa type)
- 추상자료형
- 개념적으로 어떤 동작이 있는지만 정의, 구현x
### DS(data structure)
- 자료구조
- 실제로 구현

---

## Stack
- last in first out 
- push : 넣는다
-  pop : 꺼낸다
- peek : 최상단의 값을 가져온다 

- stack memory & stack frame
	
### Error
- StackOverflowError : recursive function의 탈출조건 오류

---

## Queue
- first in first out
- enqueue : 넣는다
- dequeue : 꺼낸다
- peek

- producer/consumer architecture
- ready queue : 항상 fifo 를 의미하지는 않음
### priority queue 
- 아이템의 우선순위가 주어지는 queue , ADT
- insert : 우선순위 정보도 같이입력
- delete : 우선순위가 가장 높은 아이템을 꺼냄
- peek
	
### heap
- 주로 binary tree구조 기반으로 구현, DS
- max heap : 부모 노드의 key가 자식들의 것보다 크거나 같음
- min heap : 작거나 같음.
- insert : key값도 같이 입력
- delete : max면 key값이 가장 큰, min이면 작은 아이템을 꺼냄 = Root node
		꺼낸후에는 마지막 node의 아이템을 올리고 max상태유지
- peak
- heap은 priority queue의 구현체. (heap의 key를 우선순위로 사용)
	
### priority queue와 heap의 사용사례
- process scheduling : ready queue = priority queue
- heap sort : 다넣고 delete하면 정렬되어서 나옴

### Error
- OutOfMemoryErroer : heap memory를 다 썼을 때. 
	->큐의 사이즈를 고정.  다 차면? 
		LinkedBlockingQueue : add(e) / offer(e) / put(e) / offer(e, time, unit)
		예외 던지기 / 특별한 값(null or false)반환  / 성공할 때까지 영원히 스레드 block/제한된 시간만 블락되고 포기

---




