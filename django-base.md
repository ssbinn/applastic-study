### 장고 파일 살펴보기

settings.py에서 `ME_ZONE = "UTC" > ME_ZONE = "Asia/Seoul" 변경`
vscode 팁. intellisense라고 불림, 함수 코드에서 control 키를 누르고 있으면 해당 함수가 정의된 부분으로 갈 수 있음  

<br>

#### 장고 서버 실행
`pipenv shell 확인 > python manage.py runserver`
http://127.0.0.1:8000/ 
http://127.0.0.1:8000/admin 들어가서 확인해보기

<br>

오류가 뜬다면, 서버가 구동하지 않는 상태에서 `python manage.py migrate`
다시 서버 실행시키기 `python manange.py runserver`
username과 password를 입력하는 페이지가 뜨면 /admin 주소가 잘 작동하는 것임

<br>
#### 장고 admin 패널에 로그인
`python manage.py createsuperuser`

--- 
django migrations

migrations은 기본적으로 뭔가를 다른 쪽으로 보내는 것임
데이터베이스의 경우 하나의 상태에서 다른 상태로, 다른 데이터 유형으로 바꾸는 거야, 다시 말해 데이터의 유형이 변경될 때마다 migrate가 필요함 
장고가 이미 migrations을 생성해 둔 상태임.

`python manage.py makemigrations` 하면 장고는 우리의 models를 확인한 뒤 migration 파일을 생성하게 된다. 나의 경우 no change detected 라고 나옴, 변경된 데이터가 없기 때문임. 

장고 엔진 동작 방식
데이터 유형이 변경되면 migration을 생성하고 해당 migration을 적용, 데이터베이스를 업데이트함, (즉, 먼저 migration을 생성하고 나서 migrate) sql을 배울 필요 없이 장고가 다 알아서 해주고, 데이터베이스와 장고를 동기화할 수 있음

예를 들어 현재 user는 단순히 first_name과 last_name만 가지고 있지만 gender를 추가하려 함, gender를 추가하게 되면 우리는 migration을 생성하고 migrate를 수행하게 될 거야, 즉 데이터베이스에 한 개의 신규 column을 추가하게 될 거란 얘기

migration을 생성: `python manage.py makemigrations`
migrate를 수행: `python manage.py migrate`

--- 
우리가 만든 건 장고 프로젝트이고 여러 애플리케이션(app)을 포함함
프로젝트는 애플리케이션의 집합, 애플리케이션은 function의 집합

장고는 무언가 시작하기 전에 프로젝트를 계획하게끔 만든다
에어비앤비에서 우리가 몇 가지 애플리케이션을 만들어야 하는 지 한번 보자
1. room (숙소) 애플리케이션: room 검색하기, 생성, 삭제, 수정, room 보기
2. 예약 애플리케이션: 예약 생성, 삭제, 수정, 예약점수 보기
3. 유저 애플리케이션: 로그인, 로그아웃, 비밀번호 수정, 계정 생성 ..(장고에 이미 user 폴더가 있지만 더 확장할 필요가 있음)
등등.. 

장고를 효과적으로 사용하는 방법은 언제 애플리케이션을 만들고 또 만들지 않아야 하는 지 구분할 수 있어야 함, 팁은 한 문장으로 애플리케이션을 표현할 수 있어야 한다는 것

---
장고를 시작하게 해주는 command
airbnb_clone (버블) 폴더 안에서, config 폴더 밖에서 입력해야 함 `django-admin startapp [애플리케이션 이름]`
* 애플리케이션 이름은 반드시 복수형이어야 함

--- 
장고는 프레임워크이기 때문에 파일/폴더명은 optional이 아닌 본래 그대로여야 함

프레임워크와 라이브러리의 차이
프레임워크의 경우 프레임워크의 룰에 따라 사용해야 함
라이브러리의 경우 그저 뭔가를 빌드하기 위해 사용함 

리액트 - 라이브러리, 내가 원하는 코드내의 파일/폴더명을 마음껏 사용할 수 있음 
장고 - 프레임워크, 파일/폴더명은 optional한 게 아님 

만약 admin 패널에서 users가 어떻게 보여질지를 변경하고 싶다면 users 폴더의 admin.py에 코드를 작성
만약 URLs을 추가하고 싶으면 /config/urls.py 
장고가 urls.py를 지켜보도록 되어있기 때문
* 니꼬는 모든 url을 config의 urls.py에 넣는 것을 원하지 않음
만들 url이 너무나도 많기 때문임

내 users 애플리케이션 안에 urls.py 파일 생성 
config에 있는 urls.py로 가서 users에 있는 urls.py를 import 하는 방식으로 할 예정

---
Replacing Default User 
전에 얘기했듯이 장고는 이미 user 애플리케이션을 갖고 있음 
부족하진 않지만 확장할 필요가 있음 

username, 유효성 검사, 성, 이름, 이메일 필드들 등 이 모든 기능을 가지되 에어비앤비 user는 프로필 사진을 설정하거나 생년월일, 언어 등 확장 기능이 필요함

하지만 장고에 있는 user 애플리케이션을 대체하거나 처음부터 다 만들 필요는 없어
근데 이미 유저 데이터베이스가 장고에는 주어져 있어

장고에서는 user 모델을 덮어쓰려면 AUTH_USER_MODEL 값을 설정해야 함 
* 참고: https://docs.djangoproject.com/en/2.2/topics/auth/customizing/

우리가 할 일은 디폴트 유저 모델을 config/settings.py에서 바꿔주는 거야

먼저 모델이 뭘까 
모델은 데이터가 보여지는 모습이야, 
(/users/models.py) User 모델을 생성해보자 

그 뒤에 장고 User를 내가 만든 User로 대체해보자 
먼저 User 애플리케이션을 settings.py에서 설치해야 해, 그러면서 config/settings.py 코드를 고쳐보자 (고친 후 서버 구동)

---
user model 소개

에러 
```
ERRORS:
auth.User.groups: (fields.E304) Reverse accessor for 'User.groups' 
clashes with reverse accessor for 'User.groups'.
```
해결 - db.sqlite3 파일 삭제 후 AUTH_USER_MODEL 값 `users.User`로 설정한 뒤 서버 다시 가동 

```
ValueError: Dependency on app with no migrations: users
```
해결 - 서버 닫고, migration 만들기 `python manage.py makemigrations` > 
```
Migrations for 'users':
  users\migrations\0001_initial.py
    - Create model User
```
그리고 migrate를 수행 `python manage.py migrate`
서버를 재가동시켰을 때 더이상 에러가 나오지 않지만, /admin 주소로 접속했을 때 user가 보이지 않음 

이유는 디폴트 admin을 대체했고, 다른 model을 사용하기 때문
따라서 admin을 만들어줘야 함. 이건 장고 admin을 다뤄볼 좋은 기회임 
그 전에 user 모델을 디자인 할 거야, 데이터가 어떻게 보여져야 할 지 모델을 다뤄보자

User 모델을 user/admin.py와 연결 - admin에 user가 생김
그 안에 들어가보면 디폴트 user 페이지에 있었던 user를 만들기 위한 모든 게 갖춰졌음 (user 모델이 AbstractUser를 상속받았기 때문)

이걸 보는 이유는 이제 모델이 뭘 적을 거거든
내가 모델에 뭘 쓰든 장고가 알아서 form을 만들어 줌, 그리고 장고는 데이터베이스에다가 migration과 함께 이 form에 필요한 정보를 요청할 거야

User 모델을 user/admin.py와 연결해서 bio form이 생김
---
첫번째 모델 필드 

docstring을 배워볼 거야 파이썬에서 쓰는 표준 형식, 클래스를 만들 때마다 무슨 클래스인지 명시할 때 쓰인다

user 모델을 디자인하는 중에 `models.ImageField()` 때문에 에러가 나옴, pillow 설치 안하면 image 필드를 사용할 수 없다고 함, pillow는 이미지를 처리하는 파이썬 라이브러리임, pip로 설치하라는 문구가 뜨지만 pipenv를 사용해야 함

```python
# admin 패널에 user model 나타나게 만들기 위함
# decorator, 아래는 `admin.site.register(models.User, CustomUserAdmin)`와 같다
@admin.register(models.User)
class CustomUserAdmin(admin.ModelAdmin):

    """Custom User Admin"""

    # list_display = (
    #     "username", "language", "superhost",
    # )  # admin의 user list 페이지에서 어떤 필드를 보여줄 지 결정함

    # list_filter = (
    #     "language", "currency", "superhost",
    # )  # user 필터링

```

--- 
user 파트 복습

우리가 장고를 사용하는 게 아니라 장고가 우리 코드를 사용하는 것

장고는 장고 ORM (object relational mapping)을 탑재하고 있는데, 이게 내 파이썬 코드를 SQL 문으로 바꿔서 데이터베이스가 알아들을 수 있게 만듦

models.py에 집어넣는 것 모두 장고가 알아서 데이터베이스 테이블로 만들어줌 

Model은 fields로 이루어져 있음. char 필드, date 필드, image 필드...
image 필드의 경우 이미지 파일만 선택 가능함, 장고가 데이터 유효성 검사까지 해준다는 얘기   

Model을 직접 보려면 admin 패널에서 볼 수 있었어, admin.py에서 admin 패널의 구성을 바꿀 수 있었고, admin.py에서 Model을 가져오려면 register를 해줘야 하고, register 하기 위해선 class가 필요해. 그 class는 기본적으로 Model을 조정할 수 있어 

그리고 장고가 내가 만든 폴더를 인식하도록 하려면 setting.py에 등록해줘야 함 
장고가 원래 갖고 있는 User가 아닌 내가 만든 User를 쓰려고 `AUTH_USER_MODEL`를 바꿔줬었어 

다음으로 넘어가기 전에 데이터베이스 삭제하고, pycache 폴더가 있다면 그것도 삭제하고, migration도 삭제해야
