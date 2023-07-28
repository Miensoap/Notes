## java.util.Date
- 날짜와 시간을 다룰 목적으로 만들어진 클래스. 거의 deprecated.
## java.util.Calendar
- Date클래스를 개선한 클래스
- 추상 클래스이므로  getInstance()를 통해 구현된 객체를 얻어야함.
```
	Calendar cal = Calendar.getInsatnce(); // 현재 날짜와 시간
	
	// 메서드를 통해 상황에 맞는 객체를 반환. : 추상화
	// get(Calendar.field)
	int thisYear = cal.get(Calendar.YEAR); // 올해가 몇년인지
	int lasyDayOfMonth = cal.getActualMximum(Calendar.DATE); //  이달의 마지막날

	/*
		<날짜 관련 field>
		Year : 년
		Month : 월(0~11)
		WEEK_OF_YEAR : 그 해의 몇번째주
		WEEK_OF_MONTH : 그 달의 몇번째주
		DATE : 일
		DAY_OF_MONTH : 그 달의 몇번째일
		DAY_OF_YEAR : 그 해의 몇번째일
		DAY_OF_WEEK : 요일(1일~7토)
		DAY_OF_WEEK_IN_MONTH : 그 달의 몇번째요일

		<시간 관련 field>
		HOUR : 시간 (0~11)
		HOUR_OF_DAY : 시간(0~23)
		MINUTE : 분
		SECOND : 초
		MILLISECOND : 밀리초
		ZONE_OFFSET : GMT 기준 시차
		AM_PM : 오전/오후
	*/
```
```
	Calendar date1 = Calendar.getInstance();
	date1.set(2017,7,15); // 2017년 8월 15일
	
	long difference = (date2.getTimeInMillis() - date1.getTimeInMillis())/1000;
		System.out.println("그 날(date1)부터 지금(date2)까지"+difference+"초가 지남");

	boolean isLeapYear(int Year)
	int dayDiff(int y1,iny m1,inyd1 , int y2,int m2, int d2)
	int getDayOfWeek(int year,int month,int day)
	String convertDayToDaye(int day)
	int convertDateToDay(int year,int month, int day)

```

### Date 와 Calendar 간의 변환
```
	Date d = new Date(cal.getTimeInMillis());

	cal.setTime(d)
```

---

## 형식화 클래스
- 숫자와 날짜를 원하는 형식으로 쉽게 출력 가능 (->형식 문자열)
### DecimalFormat
```
	double number = 1234567.89;
	DecimalFormat df = new DecimalFormat("#.#E0");
	Stirng result = df.format(number); //"1.2E6"

	DecimalFormat df = new DecimalFormat("#,###.##");
	Number num = df.parse("1,234,567.89");
	double d = num.doubleValue();
```

### SimpleDateFormat
```
	Date today = new Date();
	simpleDateFormat df = new SimpleDateFormat("yyyy-MM-dd");
	String result = df.format(today); // today를 지정 format으로 변환하여 반환

	Date d = df.parse("2015-11-23"); //문자열을 Date로 변환
	Stirng result = df.formt(d); // 특정 형식으로 된 문자열에서 날짜와 시간을 뽑아냄.
```
### Choiceformat
- 특정 범위에 속하는 값을 문자열로 변환
```
	double[] limits={60,70,80,90}; // 낮은 값부터 순서로
	String[] grades = {"D","C","B",A};
	Choiceformat form = new ChoiceFormat(limits,grades);
	for (int i=0; i<scores.length; i++){
		System.out.println(scores[i]+":"+form.format(scores[i]));
		
	}
```

### MessageFormat
- 데이터를 정해진 양식에 맞게 출력
```
	String msg = "Name {0} \nTel: {1}"
	Object[] arguments = {
		"이자바","010-1234-5678"
	}
	String result = 
		MessageFortmat.format(mag, arguments);
	System.out.println(result);
```

---

## java.time패키지
- JDK1.8부터 제공

```
	// now( ), of( )를 사용해서 객체 생성
	LocalDate date = LocalDate.now(); 

	LocalTime time = LocalTime.of(23,59,59);

	// 특정 값을 얻을 때 get()
	int minute = now.getMinute();
					now.get(ChronoField.MINUTE_OF_HOUR);

	// plus( ), minus() , with( )
	LocalDate tomorrow = today.plus(1,ChronoUnit.DAYS); 
							today.plusDays(1);
```
- TemporalUnit : 날짜와 시간의 단위를 정의해 놓은 인터페이스
- ChronoUnit  : 이를 구현한 클래스
- TemporalField : 날짜와 시간의 필드를 정의해 놓은 인터페이스
- ChronoField :  구현

```
	// isAfter(), isBefore(), isEqual()
	int result = date1.compareTo(date2); // 같으면 0 이전 -1 이후 +1
```

### Instant
- 에포크타임(1970-01-01 00:00:00 UTC)부터 경과된 시간을 나노초 단위로 표시
```
	// Date와의 변환
	static Date from(Instant instant)  
	Instant toInsatant() 
```

### LocalDateTime
```
	LocalDateTime dt = LocalDateTime.of(date1,time1);

	LocalDate date = dt.toLocalDate();
							toLocalTime
```

### ZonedDateTime
```
	ZoneId zid = ZoneId.of("Asia/Seoul");
	ZonedDateTime zdt = dateTime.atZone(zid);

	ZoneOffset krOffset = ZonedDateTime.now().getOffset();
```

### TemporalAdjusters
- 자주 쓰일만한 날짜 계산을 해주는 메서드를 정의한 클래스

```
	firstDayOfNextYear()
	...
	lastDAyOfMonth()

	firstlnMonth(DayOfWeek dayOfWeek) // 이번 달의 첫 ?요일
	...
	dayOfWeeklnMonth(int ordinal, DayofWeek dow) // 이번 달의 n번째 ?요일
```

### Perioud와 Duration
```
	Period pe = Period.between(date1, date2);
```

### 파싱과 포맷
- DateTimeFormatter
```
	String yyyymmdd = 
		DateTimeFormatter.ISO_LOCAL_DATE.format(date);

	// 형식 직접 정의
	.ofPattern("yyyy/MM/dd"); 

	// 문자열 파싱
	LocalDate newDate = LocalDate.parse("2001-01-01") 
```