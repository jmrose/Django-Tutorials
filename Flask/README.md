# Flask
* SQLAlchemy ( via Flask-SQLAlchemy )
* WTForms ( via Flask-WTF )

## Flask
$ pip install flask

### Flask-WTF
>Flask-WTF ofers simple integration with WTForms. This integration includes optional CSRF handling for greater security  
$ pip install flask-wtf  

### Flask-SQLAlchemy 
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
