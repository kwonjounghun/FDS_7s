## DB  
primary key : 후보키(유일성 + 최소성) 중에서 기본적으로 사용하기 위해 선택한 키
  
## Pooling connections
연결을 준비(connection pool)해두고, 빌려 주고 받는다.  
연결 자원을 만들어두고 버리지 않아 속도가 빠르고 자원 소모가 적다.  

## JSON  
자바스크립트에서 사용 되는 방식인데, 값 전달과 DB사용 유용하다.  
반복되는 코드를 줄이고, 가독성이 좋아진다.

## insert  
insert into 테이블명(컬럼명) values(값);  
  
## update  
updat 테이블명 set 컬럼=값, 컬럼=값 where 컬럼=값

## delete
delete from 테이블 where 조건  

## select
select 컴럼명 from 테이블명

## REST 방식  
get /URL : SELECT
- get /users : select * from users
- get /users/id : select * from users where id=?

post /URL : insert, update, delete   

put /URL : update

delete /URL : delete  