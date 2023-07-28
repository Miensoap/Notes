### DBMS = Database Management Sysyem
- 계층형 : 트리 형태. 변경이 까다롭고 다른 구성원을 찾기 비효율적
- 망형 : 활용하려면 모든 구조를 이해해야함
- 관계형. RDBMS  :  열과 행으로 이루어진 테이블로 구성.  

### 데이터베이스 모델링
- 테이블 구조를 결정

### 폭포수 모델
1. 프로젝트 계획
2. 업무 분석
3. 시스템 설계
4. 프로그램 구현
5. 테스트
6. 유지보수

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

## MySQL
```
CREATE TABLE `shop_db`.`member` (
  `member_id` CHAR(8) NOT NULL,
  `member_name` CHAR(5) NOT NULL,
  `member_addr` CHAR(20) NULL,
  PRIMARY KEY (`member_id`))
COMMENT = '	';
```

```
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
```
DELIMITER //  # 스토어드 프로시저를 묶어준다
create procedure myProc() # 프로시저 이름 지정
begin
	select * from  member where member_name='아이유';
	select* from product where product_name='삼각김밥';
end //
delimiter ;

call myProc(); // 호출
```



- create / drop
```
drop procedure myProc
```
-101p