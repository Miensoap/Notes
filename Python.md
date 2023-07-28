
### 입력
```
	arr = list(map(int, input().split))
	a,b,c = map(int,input().split())
	
	# 빠르게. 
	import sys
	a  = sys.stdin.readline().rstrip() 
	
	#2차원배열 입력받기
	arr = [list(map(int, input().split())) for _ in range(B)]
```
### 출력
```
	# f-string
	print(f"정답은 {answer}입니다.")
```
### 조건문
```
	조건부 표현식 한줄에
	result = "Success" if score >=80 else "Fail"

	0<X<20 부등식 가능

	pass
```

### 반복문

### 함수
```
	# 파라미터 변수 지정 가능
	add(b=3, a=7)

	global
```

### 람다 표현식
```
	(lamda 파라미터 : 반환값)(인수)
	print((lamda a,b : a+b)(3,7))
	# lamda 표현식 안에서 변수 선언 x 바깥의 변수는 사용가능

	sorted(array, key=lambda x: x[1]) # x를받아서 x[1] 반환
	result = map(lambda a,b : a+b , list1,list2)

	list(map(lambda x : str(x) if x %3 == 0 else x ,a )
	# map(function , iterable)
	# map의 함수로 lambda를 사용

	list(filter(f,iteralbe))
	list(filter(lambda x : x>5 and x<10, a))
	# filter : iterable 객체의 요소를 함수로 처리한 뒤 반환값이 True이면 반환.
	# filter의 함수로 lambda 사용

	files = ['font', '1.png', '10.jpg', '11.gif', '2.jpg', '3.png',
	         'table.xslx', 'spec.docx']
	print(list(filter(lambda x : x.find('jpg') != -1 or x.find('png') != -1, files)))
	#lambda 함수에 x인자로 file의 요소를 받아서 x.find()를 호출. 없으면 -1 반환.
	#lambda 반환값에 조건식사용 : True or False 반환.
	#filter는 함수(lambda)의 반환값이 True면 요소를 반환. -> list에저장.

	from functools import reduce
	reduce(f,iterable)
	reduce(lambda x,y : x+y , a)
	# reduve : iterable 객체의 요소를 함수로 처리한 뒤 이전 결과와 누적해 반환.
	
	
```
### list 표현식
```
	a = [i for i in a if i>5 and i<10]
```