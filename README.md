YTD_Project_02
==
Board with MongoDB

## 1. MongoDB 설치
- [MongoDB 사이트](https://www.mongodb.com/download-center#community)에서 다운로드 후 설치
> ```C:\Program Files\MongoDB\Server\3.6\bin```에 설치 됨
- 데이터 베이스 저장 경로 설정 및 MongoDB 실행
```bash
$ mkdir "C:\mongodb"
$ cd "C:\mongodb"
$ mkdir data
$ mkdir log
$ "C:\Program Files\MongoDB\Server\3.6\bin\mongod.exe" --port 27017 --dbpath "C:\mongodb\data"
```
- MongoDB 접속
```bash
$ "C:\Program Files\MongoDB\Server\3.6\bin\mongo.exe" --port 27017
```
- admin 계정 생성
```bash
> use admin
> db.createUser(
... {
... user: "admin",
... pwd: "p@ssw0rd",
... roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
... })
```
- MongoDB 재실행
```bash
$ "C:\Program Files\MongoDB\Server\3.6\bin\mongod.exe" --port 27017 --auth --dbpath "C:\mongodb\data"
```
- admin 계정으로 로그인
```bash
$ "C:\Program Files\MongoDB\Server\3.6\bin\mongo.exe" --port 27017 -u "admin" -p "p@ssw0rd" --authenticationDatabase "admin"
```
- 실 사용 계정 생성
```bash
> use test
> db.createUser(
... {
... user: "ytd",
... pwd: "p@ssw0rd",
... roles: [ { role: "readWrite", db: "test" } ]
... }
... )
```
- MongoDB 서비스 등록
```bash
# mongod.conf 파일 생성
systemLog:
    destination: file
    path: c:\mongodb\log\mongod.log
storage:
    dbPath: c:\mongodb\data
security:
  authorization: enabled
```
```bash
# 서비스 등록
$ "C:\Program Files\MongoDB\Server\3.6\bin\mongod.exe" --install --serviceName "MongoDB 3.6" --serviceDisplayName "MongoDB(로컬 개발용)" --serviceDescription "YTD 프로젝트 개발용" --config "C:\mongodb\mongod.conf"
 ```

## 2. Project 초기화
```bash
$ npm install -g express
$ npm instlal -g express-generator
$ express --view==ejs .
$ npm install nunjucks --save
$ npm install
```

app.js 파일 수정
```js
var nunjucks = require('nunjucks');

// view engine setup
nunjucks.configure("views", {
  autoescape: true,
  express: app
});
app.set("view engine", "nunjucks");
```
index.html 파일 추가



## 3. bootstrap & jquery 설치
 ```bash
 $ npm install bootstrap@3.3.7 jquery --save
 ```

```javascript
app.use('/js', express.static(__dirname + '/node_modules/bootstrap/dist/js')); // redirect bootstrap JS
app.use('/js', express.static(__dirname + '/node_modules/jquery/dist')); // redirect JS jQuery
app.use('/css', express.static(__dirname + '/node_modules/bootstrap/dist/css')); // redirect CSS bootstrap
```

