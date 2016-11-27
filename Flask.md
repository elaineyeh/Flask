# Flask

## 安裝 Flask

### Step.1 在終端機安裝 pip
`sudo pacman -S python-pip`
### Step.2 用 pip 裝 Flask
`sudo pip install Flask`
#### 就完成 Flask 的安裝拉～

---
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
---
## 使用樣板 template

### 在 Hello.py 的目錄下建一個資料夾名稱一定要是 template
`mkdir template`
### 寫一個 HTML 檔在資料夾底下（在這裡用 test.html）
```html
<!doctype html>
<title>Hello from Flask</title>
{% if template_name %}
  <h1>Hello {{ template_name }}!</h1>
{% else %}
  <h1>Hello, World!</h1>
{% endif %}
```

### 新建一個檔輸入以下程式碼
```py
from flask import Flask
from flask import render_template
app = Flask(__name__)

@app.route('/hello/')
@app.route('/hello/<name>')
def hello_use_template(name=None):
    # 第一個參數是在 templates 資料夾下你要使用的 樣版 檔案
    # 第二個參數是你要傳給 樣版 解析代入的資料
    # 第二個參數前面的 template_name 是樣板中的變數
    # 第二個參數後面的 name 是這個 hello_use_template 函數中的變數
    return render_template('test.html', template_name=name)
if __name__ == "__main__":
    app.run()
```
### 在瀏覽器開啟網頁
http://127.0.0.1:5000/elaine
#### template 會把 name 帶給 template_name ,所以 template_name -> name -> elaine
#### 因為 name 有東西,所以在 HTML 裡面 if 成立的,所以會出現 Hello elaine !

---

## 使用 Markup 選擇輸出是 HTML 標籤還是 文字
### 新建一個檔輸入以下程式碼
#### 記得 'from flask import Markup'
```py
from flask import Flask
from flask import render_template
from flask import Markup
app = Flask(__name__)

@app.route('/html/br')
def br():
    return Markup('<h1>一級 %s 標籤.</h1>') % '</br>'

@app.route('/html/h1')
def h1():
    return Markup.escape('<h1> 一級標籤. </h1>')

@app.route('/html/none_tag')
def none_tag():
    return Markup('<p> HTML 標籤會被移除</p> &raquo 但是特殊符號不會').striptags()

if __name__ == "__main__":
    app.run()
```
### 在瀏覽器開啟網頁  

http://127.0.0.1:5000/html/br  
```
在原始碼中
在 Markup 函式中 <h1></h1> 不變
但是放入的 <br> 會變成 &lt;/br&gt;
所以字會放大成一級標籤,而 <br> 標籤還是顯示 <br>
```


http://127.0.0.1:5000/html/h1
```
在原始碼中
< 這個符號變成 &lt;
> 這個符號變成 &gt;
所以字不會放大, <h1> 標籤還是顯示 <h1>
```
`<h1> 一級標籤. </h1>`

http://127.0.0.1:5000/html/none_tag
```
在原始碼中
只要是 HTML 的標籤皆會被刪除
但是特殊符號可以
所以字不會顯示 <p> 但是可以顯示 &raquo 的特殊符號
```
`HTML 標籤會被移除 » 但是特殊符號不會`
