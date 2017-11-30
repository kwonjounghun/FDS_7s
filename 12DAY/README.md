# 2017. 11. 28 수업 내용 정리
## node.js
* 한때 Explorer 가 브라우저 시장을 지배했으나 Chrome이 나오면서 상황이 바뀜
* Chrome의 성능 -> V8 engine
* Ryan Dahl - V8로 node.js를 만듬
* node의 장점 -> V8의 성능 발전에 따라 계속 좋아질 것

기계 >>>>>>>>>>>>>>>>>>>> 인간  
기계어 -> 어셈블리 -> C -> C++ -> Java

## C 언어
* if / for 문이 여기서 처음 생김

## Object Oriented Programming
* 추상화 : 속성 + 행위
* 명사 + 동사
* 변수 + 메소드
* GUI 시대를 맞아 모든 것을 지배함
* 그러나 동시 처리 갯수가 많아지면 -> 성능 저하

## 함수형
* 객체지향
 * C++
 * Java
* 하이브리드
 * JS
 * Py
 * Ruby
 * Swift
 * Kotlin
* 함수형
 * Haskell 등

## 함수형 언어가 제공하는 머시기들 :
### map / filter / reduce
* map : 하나씩 처리
* filter : 걸러내기
* reduce : 줄임 // 예: 합계 라던지
* 이상을 선언적인 코딩이라고 함

##HTTP 내 서버 전달 방식 
* et
* ost
* 쿠키 : PC에 *.txt로 저장
* 세션 : 서버 메모리에 생기는 키(보안이 됨) : 값 (id : hong), 장바구니(상품코드 : 수량)


* fav(orite)icon

##  Database 모델링
1. 논리적인 모델링  
 * 게시판 테이블
 * 글번호
 * 제목
 * 내용
 * 작성자
 * 날짜
 * 조회수
 * 비밀번호
 * 글번호

2. 물리적인 모델링
  * board
   * num -> int
   * subject -> varchar(100)
   * content -> text
   * writer -> text -> varchar(20)
   * regdate -> datetime
   * hit -> int
   * pwd -> varchar(20)
   * primary key

cf) 숫자 int / 문자 varchar, text / 날짜: datetime종이에 논리 모델링 -> 물리 모델링 -> Query



###  AWS
  1. EC2 : 가상 머신
  2. S3 : Simple Storage Service : 외장하드 임
  3. RDS : Relational Database Service : DB

### EC2 인스턴스에 nvm, express, pm2 설치하기

mac/linux/win10:
```
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.6/install.sh | bash
```
curl  <- 인터넷으로 다운받
|        <- 아서
bash <- 실행
```
chmod 400 FDS-CS-board.pem
```
```     
ec2-13-124-78-73.ap-northeast-2.compute.amazonaws.com
```


windows :
 0. putty를 써야 함
 1. ~.pem -> ~.ppk
 2. putty 실행 / 설정

EC2 ubuntu에 접속해서 일단 ubuntu 업데이트를 해주고,
```
sudo apt-get update
```
아래와 같이 nvm을 설치한다.
```
$ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.6/install.sh | bash
```
하지만 이것만으론 실행이 되지 않으므로,  ubuntu 터미널 내장 에디터 nano를 사용해 .bashrc를 편집해줘야 함.
```
nano .bashrc
```
로 .bashrc 파일을 열어 아래 코드를 마지막에 붙여넣기 해준다.
```
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" # This loads nvm
```
(우클릭을 하면 paste 까지 됨)
저장 후 아래 명령으로 restart 없이 nvm을 바로 사용할 수 있다.
```
$ source ~/.bashrc
```
이후의 순서는 아래와 같음.
```
$ nvm install 8.9.1
$ node -v
$ npm i -g express-generator
$ mkdir projects
$ cd projects
$ express --ejs exp1
$ cd exp1
$ npm i
$ npm start
```
만든 앱이 서버에서 계속 돌 수 있도록 pm2를 설치해준다.
```
$ npm i -g pm2
```
bin 폴더를 삭제하고
```
$ rm -r bin
```
app.js에 아래 코드를 추가해준다.
```
$ nano app.js
```

```
app.listen(3000);
console.log(“Server started!!!“);
```
cat 명령으로 app.js의 내용을 알아볼 수 있다.
```
$ cat app.js
```
pm2로 다시 서버를 실행해준다.
```
$ pm2 start app.js
$ pm2 stop app
```