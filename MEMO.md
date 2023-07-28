<span style="color:red"> 
hi<br>
<br>
</span>
입력
```
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
int[] arr = Stream.of(br.readLine().split(" ")).mapToInt(Integer::parseInt).toArray();

// parseInt 대신 valueOf?
```
Comparator
``` 
// 리스트 정렬
List<Integer> list = new ArrayList<>();
Collections.sort(list,Comparator.comparingInt9(a->a));
// 우선순위큐 생성
PriorityQueue<Integer> que = new PriorityQueue<Integer>(Comparator.comparingInt(o->o));
```
