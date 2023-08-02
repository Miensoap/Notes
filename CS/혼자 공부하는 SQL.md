### DBMS = Database Management Sysyem
- 계층형 : 트리 형태. 변경이 까다롭고 다른 구성원을 찾기 비효율적
- 망형 : 활용하려면 모든 구조를 이해해야함
- 관계형. RDBMS  :  열과 행으로 이루어진 테이블로 구성.  

### 데이터베이스 모델링
- 테이블 구조를 결정

### 용어
- Data : 하나하나의 단편적 정보
- Table : 데이터를 입력하기 위해 표 형태로 표현
- Database : 테이블이 저장되는 저장소
- DBMS : 데이터베이스 관리 시스템
- column : 테이블의 세로. 열
- 데이터 형식 : 테이블 생성시 열 이름과 함께 지정
- row : 실질적 데이터.
- Primary Key : 기본키. 각 행을 구분하는 유일한 열. 중복되거나 비어있으며 안됨
- SQL : Structured Query Language 구조화된 질의 언어

### DB생성 -> 테이블 생성 -> 데이터 입력/수정/삭제 -> 조회/활용
---
## MySQL
```MySQL
CREATE TABLE `shop_db`.`member` (
  `member_id` CHAR(8) NOT NULL,
  `member_name` CHAR(5) NOT NULL,
  `member_addr` CHAR(20) NULL,
  PRIMARY KEY (`member_id`))
COMMENT = '	';
```

```MySQL
# select col_name from table_name [where 조건]
# ctrl shift enter
-- select * from member;
select member_name, member_addr from member;
```

- Schema = db

### Database Object
- Table
- index :
	- non-unique key lookup =Full Table Scan
	- <-> key lookup = Index Scan
- view : 가상의 테이블. 보안에 도움이 된다. 문장을 간략하게 할수있다.
	- =select문. 
- stored procedure : 여러개의 sql문을 하나로 묶어서 사용가능.
```MySQL
DELIMITER //  -- 스토어드 프로시저를 묶어준다
create procedure myProc() -- 프로시저 이름 지정
begin
	select * from  member where member_name='아이유';
	select* from product where product_name='삼각김밥';
end //
delimiter ;

call myProc(); // 호출
```

---
### DB  생성/삭제
```MySQL
DROP DATABASE IF EXISTS market_db;
CREATE DATABASE market_db;
```
- create / drop
```MySQL
drop procedure myProc
```
---
### SELECT
- SELECT ~ FROM ~ WHERE
-  *  : 모두
```MySQL
SELECT *FROM member;
	WHERE mem_number = 4; -- 조건식
		BETWEEN ~ AND
		IN( )
		AND OR
		LIKE '우%'; -- 첫글자가 '우'이고 뒤는 '%' 무엇이든
			'__핑크';
			
	ORDER BY debut_date;
		DESC -- 내림차순
		ASC -- 오름차순(기본)
```
- ORDER BY절은 WHERE 절 뒤에 나와야한다 
```MySQL
	LIMIT 3, 2; -- 시작, 개수

	DISTINCT -- 중복된 데이터를 제거
	
	GROUP BY mem_id; -- 같은 데이터끼리 묶어서
	-- 주로 집계 함수와 함꼐 사용
		SUM()
		AVG()
		MIN()
		MAX()
		COUNT()
			COUNT(DISTINCT)
		SELECT mem_id, SUM(amount) FROM buy GROUP BY mem_id;
		SELECT mem_id "회원 아이디" -- 별칭 사용
			SUM(price*amount) "총 구매 금액"
	
	HAVING 조건식
	-- 조건식에 집계함수를 사용할 때
		HAVING SUM(price*amount) >1000;
	
```

---
### INSERT
```MySQL
INSERT INTO 테이블[(열 1, 열2, ...)] VALUES (값1, 값2, ..)
```
##### AUTO_INCREMENT
- 1부터 증가하는 값을 입력
- 꼭 PRIMARY KEY로 지정해야함
```MySQL
CREATE TABLE hongong2(
	toy_id INT AUTO_INCREAMENT PRIMARY KEY, 
		-- AUTO_INCREMENT = 100; 시작 값 변경
	toy_name CHAR(4),
	age INT
);

SET @@auto_increment_increment = 3; -- 증가값 변경

INSERT INTO hongong2 VALUES (NULL,'보핍',25);

INSERT INTO city_popul
	SELECT Name, Population FROM world.city; -- 다른 테이블로부터 입력

SELECT LAST_INSERT_ID(); -- 마지막 숫자 확인
```
---
### UPDATE
- 입력되어 있는 데이터를 수정
```MySQL
UPDATE city_popul;
	SET city_name = '서울' , population =0 
	WHERE city_name = '서울'; -- WHERE 이 없으면 모든 행의 값이 변경
-- 
```
---

### DELETE
```MySQL
DELETE FROM city_popul
	WHERE city_name LIKE 'New%';
	LIMIT 5;
-- 느림. 조건문 사용 가능.

DROP TABLE big_table; -- 테이블 자체를 삭제. 빠름
TRUNCATE TABLE big_table; -- 빈 테이블을 남김. 빠름. 조건문 사용 불가

```
---

## 데이터 형식
