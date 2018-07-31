
# Django  
  
### Install
$ pip install Django  
  
### Tutorial
* Part 1: Requests and responses
* Part 2: Models and the admin site
* Part 3: Views and templates
* Part 4: Forms and generic views
* Part 5: Testing
* Part 6: Static files
* Part 7: Customizing the admin site


### Command

* __migrate__  
_- 계정, 권한, 그룹등 장고 어드민의 필수 테이블을 생성한다._  
$  ~/.pyenv/versions/app/bin/python manage.py migrate  
  
* __makemigrations__  
_- 모델을 변경시킨 사실과 이 변경사항을 migration으로 저장시키고 싶다는 것을 Django에게 알려줍니다_  
$ ~/.pyenv/versions/app/bin/python manage.py makemigrations polls  
  
* __inspectdb__  
_- 이미 운영중인 테이블로 모델 클래스 생성_  
$ ~/.pyenv/versions/app/bin/python manage.py inspectdb member member_sub > member/models.py  
  
### Django API ( Django Rest Framework )
