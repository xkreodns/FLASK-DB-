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
