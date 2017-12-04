# What is Database?
a collection(relation) of data tables

## Feature of DB

1. PK
Primary Key : 모든 table에는 pk가 있고, pk가 항상 기준.
pk는 다른 table의 foreign key가 된다

2. 관계
1:1 관계, 1:다 관계 가능하지만 다:다 관계는 없다
다:다 관계를 만들기 위해 중간에 연결을 둔다.

e.g 수강신청
학생(여러명) - 과목(여러개)   중간에 학생 - 수강신청 - 과목 으로 해소



## Maria DB setup
When setting up, click utf-8



## RDBMS
Relational DB Management System



### mobile server   vs web server

mobile server 결과를 json으로 - res.json

web server는 결과를 html로 - html을 변환할 때는 res.render 


### package.json

dependencies가 내가 필요한 module에 관한 정보
if no package.json, 8줄 모두 코딩해야함.

e.g.
npm: body-parser 등등 8줄 다 해줘야 함




### DB creation example - board
```
create table board(
    num int not null auto_increment,
    pwd varchar(20) not null,
    subject varchar(100) not null,
    content text not null,
    writer varchar(20) not null,
    regdate datetime not null default now(),
    hit int not null default '0',
    primary key(num)
)
```

### DB creation example - member
```
create table member(
    id varchar(20) not null,
    name  varchar(20) not null,
    email varchar(50) not null,
    tel varchar(13) not null,
    primary key(id)
);
```



## DB commands on Node
### insert
const sql = "insert into member(id, name, email, tel) values(?, ?, ?, ?)";
const arr = ['hong', '홍길동', 'hong@a.com', '010-1234-5678']

> command : insert into member (id, name, email, tel)
> value   : ('hong', '홍길동', 'hong@a.com', '010-33-33')


### update
const sql = "update member set name=?, email=?, tel=? where id=?";
const arr = ['홍길순순순순', 'soon@a.com', '010-1111-2222', 'hong'];

UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;

The WHERE clause specifies which record(s) that should be updated. If you omit the WHERE clause, all records in the table will be updated!

### delete

const sql = "DELETE FROM member WHERE id=?";
const arr = ['hong'];

DELETE FROM table_name
WHERE condition;

The WHERE clause specifies which record(s) that should be deleted. If you omit the WHERE clause, all records in the table will be deleted!

### select

The SELECT statement is used to select data from a database.
SELECT * 모든 데이터를 불러오나 느려질 수 있음.




### nodemon app.js


### 
select * from board order by num desc

desc = descending



### aws - ubuntu maria db setup
해당 폴더로 이동
https://downloads.mariadb.org/mariadb/repositories/


aws ec2 connect에서 보는 것

ssh -i "fastcampus.pem" ubuntu@ec2-13-124-173-60.ap-northeast-2.compute.amazonaws.com
는 3단계로 나뉜다

ssh -i "fastcampus.pem"    

ubuntu@ec2-13-124-173-60

.ap-northeast-2.compute.amazonaws.com


### aws에서 maria db 직접 설치 보다는 rds를 쓰는게 편하다


### 터널링 aws에서 heisql 보는 법
mysql -uroot -p
password 입력

mariaDB [(none)]>  show database;
mariaDB [(none)]>  create database test;
mariaDB [(none)]>  show database

>aws에서 3306포트를 열어두면 해킹당해서 망함
heisql 가서 고급기술 사용
네트워크 유형에서 mysql (ssh tunnel) 을 클릭
ssh tunnel에서 plink에 putty의 plink.exe를 넣어줘라
ssh 호스트 + 포트 넣기 aws ip주소 및 포트는 22

사용자이름 ubuntu
암호는 빈칸
개인키에는 ppk 넣어주기
로컬포트 3306

---
---


sql 명령어 정리
===


```sql
-- CREATE(테이블 생성)

CREATE TABLE tablename (
    column_name1 INT AUTO_INCREMENT,
    column_name1 VARCHAR(15) NOT NULL,
    column_name1 VARCHAR(15),
    column_name1 INT
)


-- INSERT(값 삽입)

INSERT INTO tablename VALUES(값1, 값2, ...);

INSERT INTO tablename (col1, col2, ...) VALUES(값1, 값2, ...);


-- SELECT(테이블 컬럼 선택)

SELECT col1, col2, ... FROM tablename;

SELECT col1 AS '성명', col2 AS '국어점수' FROM tablename;
SELECT * FROM tablename ORDER BY col1 DESC;
SELECT col1, korean + math + english AS `총점` ASC;
    --컬럼명을 *로 하면 모든 컬럼을 선택한다
    --ORDER BY col1 DESC - 내림차순
    --ORDER BY col1 ASC - 오름차순
    --AS 뒤에 나오는 값은 일름을 바꿔서 출력한다. (별명)

SELECT * FROM grade WHERE korean < 90;
    --WHERE - 조건을 준다.

SELECT * FROM grade LIMIT 10;
SELECT * FROM grade LIMIT 100, 10;
    --LIMIT 10 - 결과중 처음부터 10개의 값만 가져온다.
    --LIMIT 100, 10 - 결과중 100번째부터 10개의 값만 가져온다. 


-- UPDATE(테이블 컬럼 수정)

UPDATE tablename SET col1=새값 WHERE 조건


--DELETE(테이블 컬럼 삭제)

DELETE FROM tablename WHERE col1=1
    --col1의 값이 1인 행을 삭제한다.
```

