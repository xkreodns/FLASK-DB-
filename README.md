# FLASK-DB-

<img src="https://user-images.githubusercontent.com/116257795/229431886-159aa356-75a5-4d77-bf95-c527d97d1d0d.png" height="400px">

``` python
from flask import Flask, request, render_template  
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello World!'

@app.route('/hi')
def hellohtml():
    return render_template("index.html")

if __name__ == '__main__':
    app.run()
```

PRIMARY KEY
이미 테이블을 만든경우
1. ALTER TABLE (테이블이름 test)

   MODIFY COLUMN 필드이름(phone) 필드타입int(10) PRIMARY KEY
   
<img src="https://user-images.githubusercontent.com/116257795/229434016-9e018672-998a-43b6-9c2a-78b11fa61bef.png" height="200px">

이미 table 있는경우 외래키
ALTER TABLE (테이블이름 test1) ADD FOREIGN KEY (필드이름 참조)
REFERENCES 테이블이름 test (필드이름 phone)


<img src="https://user-images.githubusercontent.com/116257795/229435606-b2b5f129-caa1-4c05-8540-852c5e9c1510.png" height="200px">



1.db 설치
sudo apt-get install mariadb-server
2.db 접속
sudo mysql -u root
3.root 비밀번호 설정
alter user 'root'@'localhost' identified by '1234';
4.나간후 재접속
나가기 : CTRL + C
재접속 : mysql -u root -p
5.db생성 및 사용
create database test;
use test;
6. 테이블 생성 - 센서 데이터 , 현재 시간을 컬럼으로 한 테이블
create table sensordb(
sensing INT,
ts TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATA CURRENT_TIMESTAMP
);
7데이터 삽입
insert into sensordb(sensing) values(1023);
select*from sensordb;

<img src="https://user-images.githubusercontent.com/116257795/229705353-ca59d3d3-f6a9-4aa7-bcb1-d29a38e0f99d.png" height="200px">

<img src="https://user-images.githubusercontent.com/116257795/229705420-6c992a69-afd6-4417-abdc-f6d4ced09604.png" height="200px">


[2]Pthon 에서 DB연결
1. 모듈 import 
sudo pip3 install PyMySQL
2.MYSQL 연결
import pymysql as ps
import pandas as pd

con = ps.connect(
    host='localhost', 
    user='root',
    password='1234', 
    db='test', 
    charset='utf8',
    autocommit=True,
    cursorclass=ps.cursors.DictCursor
)

cur = con.cursor()



2.MYSQL 연결확인 - 특정테이블 불러오기
cursor = db.cursor()

def insertSensor(sensor) :
    sql = f"insert into sensordb(sensing) values({sensor})"
    cursor.execute(sql)
    db.commit()

3. 데이터 삽입

cursor = db.cursor()

def insertSensor(sensor) :
    sql = f"insert into sensordb(sensing) values({sensor})"
    cursor.execute(sql)
    db.commit()
    
전체코드 
import pymysql as ps
import pandas as pd

con = ps.connect(
    host='localhost', 
    user='root',
    password='1234', 
    db='test', 
    charset='utf8',
    autocommit=True,
    cursorclass=ps.cursors.DictCursor
)

cur = con.cursor()

def insertSensor(sensor) :
    sql = f"insert into sensordb(sensing) values({sensor})"
    cur.execute(sql)
    con.commit()

insertSensor(500)

# 특정 테이블 불러오기
sql = "SELECT * FROM sensordb" # sensordb 테이블 전체를 불러옴
cur.execute(sql)
rows = cur.fetchall()
customers = pd.DataFrame(rows)
con.close() # DB 연결 종료
# print(rows)
print(customers)

<img src="https://user-images.githubusercontent.com/116257795/229706098-2ca4cf3a-2d9d-40ee-9873-4556337513f2.png" height="200px">



FLASK 사용하기
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello():
    return 'Hello World!'

if __name__ == '__main__':
    app.run()
    

<img src="https://user-images.githubusercontent.com/116257795/229706266-b3bf40e5-ec20-4bf8-8c98-72d106019786.png" height="200px">

html과 flask 연동되는지 확인



