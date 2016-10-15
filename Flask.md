# Flask

## 安裝 Flask

### Step.1 在終端機安裝 pip
`sudo pacman -S python-pip`
### Step.2 用 pip 裝 Flask
`sudo pip install Flask`
#### 就完成 Flask 的安裝拉～


## Hello World

### 先寫一個檔 hello.py
```py
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return 'Hello World'

if __name__ == "__main__":
    app.run()
```

### 在終端機執行
`python hello.py`  
\* Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)

### 在瀏覽器開啟網頁
http://127.0.0.1:5000/


## 從網址取得參數
```
從 <username> 取得參數
參數前面及參數部份都不可以重複
```
```py
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return 'Hello World'

@app.route("/user/<password>")
def show_username(password):
    if password == '123':
       return '''
       <marquee>Hello World</marquee>
       '''
    return 'Error'



if __name__ == "__main__":
    app.run()
```


## 可以在 return 裡面寫 html !

```py
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return 'Hello World!'

@app.route("/user/<username>")
def show_username(username):
    return '''
    <marquee>Hello World</marquee>
    '''

@app.route("/pass/<password>")
def show_post_ip(password):
    return '''
    <hr size="5" align="left" noshade width="85%" color="#D4D4D4">
    <hr size="7" align="center" noshade width="90%" color="#A3A3FF">
    <hr size="5" align="right" noshade width="80%" color="#A1A1A1">

    <h1 align="center">Hi! Welcome to my Web~</h1>

    <hr size="5" align="right" noshade width="85%" color="#A1A1A1">
    <hr size="7" align="center" noshade width="90%" color="#A3A3FF">
    <hr size="5" align="left" noshade width="80%" color="#D4D4D4">
    '''

if __name__ == "__main__":
    app.run()
```
