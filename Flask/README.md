# Flask

* Flask 설치
* 글로벌객체 g
* HTTP 요청 핸들러
* make_response
* Routing
* Request
* 유용한 middleware

#### Flask 설치
$ pip install flask  
  
#### 글로벌객체 g
> 웹 애플리케이션이 동작하는 동안 유지되어야 하는 값을 저장한다.  
  
#### HTTP 요청 핸들러
* before_first_request : 웹 애플리케이션 기동 이후 가장 처음 http 요청에 실행
* before_request : http 요청이 들어올때 마다 실행
* after_request: http 요청이 끝나 브라우저에 응답하기 전에 실행
* teardown_request : 브라우저에 응답한 다음에 실행
* teardown_appcontext: 요청이 완전히 완료되면 실행

#### make_response
> 사용자 응답 객체를 반환하기
- ResponseClass 
```code
from flask import Response, make_response

@app.route("/")
ref response_app():
   response = Response("response", 200, {
     "Program": "Flask Web Application"
   })

   return make_response(response)
 ```
 - str 문자열 사용  
  : return make_response("str 문자열")  
    
 - unicode 문자열 사용    
  : return make_response(u"Unicode 문자열").
 
 - wsgi function 사용


#### Routing
@app.route('/', methods=['GET', 'POST'])  
  
@app.route('/', methods=['GET'])  
method 지정이 없으면 기본 Get만 허용됨  
post 요청 시, 405 Method Not Allowed 메시지와 상태코드가 응답됨 
  
@app.route('/')  
route 데코레이터에 두번째 인자를 전달하지 않으면 기본적으로 endpoint 인자로 인식한다.  

> add_url_rule 메서드는 뷰 함수를 미리 만들어 놓고 라우팅 지정을 하려 할 때 사용한다.  
add_url_rule 메서드는 대규모 애플리케이션 제작 시에 특정 라우팅을 빼고 싶을 때 유용하다    
app.add_url_rule("/", "index", index) : 인자이름과 값을 지정하지 않으면, 순서대로 처리할 Url, alias, 뷰 함수 객체로 인식  
route 데코레이터와 add_url_rule 메서드는 기능차이보다 관리 차이  

```route
Routing Option

* default option
  : routing 데코레이션에 default 값을 지정하여 전달할 수 있다.
  @app.route("board/<article_id>")
  @app.route("board", defaults={"article_id":10})

* method option
  : http 메서드를 타입에 맞게 전달할 수 있다. ( GET, POST, HEAD, PUT, TRACE, CONNECT, DELETE, OPTIONS )
  @app.route("board", method=["GET", "POST"])
  
* host option
  : 라우팅 뷰 함수가 응답할 서버 도메인을 지정할 수 있다. ( url_map.host_matching : True 로 설정해야 한다. )
  @app.route("board", host="example.com")
  @app.route("board", host="example2.com")  // 한개 이상 등록이 가능
  
* subdomain option
  : 서브 도메인별로 라우팅이 가능하다.
  @app.route("board", subdomain="blog")  // blog.example.com
  def test():
   return ""
   
  : 다수 서브 도메인 등록이 가능하다.
  @app.route("board", subdomain="cafe")
  @app.route("board", subdomain="blog")

* redirect_to option
  : 강제로 다른 화면을 전달할 수 있다.
  @app.route("board", redirect_to="other_board")
  
  @app.route("other_board")  

```
  
#### Request
* request.args.get  
  : methos = ['GET']  
  
* request.form.get  
  : method = ['POST']  
    
* request.values.get("param", 1, type=int)   
  : method = ['GET','POST']

> type은 자료형도 되지만, function, class도 가능하다  

* type >>> function  
  
```function  
def dateTypeFunc(date):  
  return datetime.strptime(...)  
  
@app.route("/")  
def board():  
  request.values.get("date", "2018-09-04", type=dateTypeFunc("%Y-%m-%d"))  
  return ""  
```
  
* type >>> class  
 
```class
class dateTypeClass:
  def __init__(self, format):
    self.format = format
    
  def __call__(self, *args, **kwargs):
    return datetime.strptime(args[0], self.format)
    
@app.route('/')
def board():
  request.values.get("date", "2018-09-04", type=dateTypeClass("%Y-%m-%d"))
  return ""
```

> request.args, request.form, request.values 에 저장된 data는 MultiDict(ImmutableMultiDict) 데이터 타입을 갖는다

__MultiDict 관련 메서드__
* get, getlist
* set, setlist
* add, pop

__environ___
> http 통신에서 사용되는 환경 변수를 담고 있는 사전  


### 유용한 Middleware
* SQLAlchemy ( via Flask-SQLAlchemy )
* WTForms ( via Flask-WTF )


#### Flask-WTF
>Flask-WTF ofers simple integration with WTForms. This integration includes optional CSRF handling for greater security  
$ pip install flask-wtf  

#### Flask-SQLAlchemy 
>Adds SQLAlchemy support to Flask. Quick and easy  
$ pip install flask-sqlalchemy

SQLAlchemy 에러 :  
Import error :No module named MYSQLdb
  
$ pip install mysqlclient  // 설치

```error
    building '_mysql' extension
    error: Microsoft Visual C++ 14.0 is required. Get it with "Microsoft Visual C++ Build Tools": https://visualstudio.microsoft.com/downloads/
    
설치 시 에러날 경우,  미리 컴파일된 pip용 whl파일로 설치
download url >>>  https://www.lfd.uci.edu/~gohlke/pythonlibs/#mysqlclient
$ pip install mysqlclient-1.3.13-cp37-cp37m-win_amd64.whl
    
```
