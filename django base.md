<br>

### 장고 파일 살펴보기

settings.py에서 `ME_ZONE = "UTC" > ME_ZONE = "Asia/Seoul" 변경` <br>
vscode 팁. intellisense라고 불림, 함수 코드에서 control 키를 누르고 있으면 해당 함수가 정의된 부분으로 갈 수 있음  

<br>

#### 장고 서버 실행
`pipenv shell 확인 > python manage.py runserver` <br>
http://127.0.0.1:8000/  <br>
http://127.0.0.1:8000/admin 들어가서 확인해보기 

<br>

오류가 뜬다면, 서버가 구동하지 않는 상태에서 `python manage.py migrate` <br>
다시 서버 실행시키기 `python manange.py runserver` <br>
username과 password를 입력하는 페이지가 뜨면 /admin 주소가 잘 작동하는 것

<br>

#### 장고 admin 패널에 로그인
`python manage.py createsuperuser`

<br>

### django migrations

migrations은 기본적으로 뭔가를 다른 쪽으로 보내는 것 <br>
데이터베이스의 경우 하나의 상태에서 다른 상태로, 다른 데이터 유형으로 바꾸는 거야, 다시 말해 데이터의 유형이 변경될 때마다 migrate가 필요함 <br>
`python manage.py makemigrations` 하면 장고는 우리의 models를 확인한 뒤 migration 파일을 생성한다. 해보면 no change detected 라고 나오는데, 변경된 데이터가 없기 때문 

<br>

#### 장고 엔진 동작 방식
데이터 유형이 변경되면 migration을 생성하고 해당 migration을 적용, 데이터베이스를 업데이트함, (즉, 먼저 migration을 생성하고 나서 migrate) <br>
sql을 배울 필요 없이 장고가 다 알아서 해주고, 데이터베이스와 장고를 동기화할 수 있다.

<br>

migration을 생성: `python manage.py makemigrations` <br>
migrate를 수행: `python manage.py migrate`

<br>

### 장고 애플리케이션
우리가 만든 건 장고 프로젝트이고, 여러 애플리케이션(app)을 포함한다. <br>
프로젝트는 애플리케이션의 집합, 애플리케이션은 function의 집합 

<br>

장고는 무언가 시작하기 전에 프로젝트를 계획하게끔 만든다. 몇 개의 애플리케이션을 만들어야 하는 지, 그리고 애플리이션 내 함수는 어떤 걸 만들어야 하는 지 등 <br>
장고를 효과적으로 사용하기 위해서는 언제 애플리케이션을 만들고 또 만들지 않아야 하는 지 구분할 수 있어야 하고, 한 문장으로 애플리케이션을 표현할 수 있어야 한다.

<br>

#### 애플리케이션 생성
(버블) 폴더 안에서, config 폴더 밖에서 입력해야 함 `django-admin startapp [애플리케이션 이름]` <br>
이때 애플리케이션 이름은 반드시 복수형이어야 한다.

<br>

추가로 장고는 프레임워크이기 때문에 파일/폴더명은 optional이 아닌 본래 그대로여야 한다. <br>
프레임워크와 라이브러리의 차이는 <br>
프레임워크의 경우 프레임워크의 룰에 따라 사용해야 하고, 라이브러리의 경우 그저 뭔가를 빌드하기 위해 사용한다. <br>
그래서 라이브러리인 리액트의 경우 파일/폴더명이 optional 하지만, 장고는 그렇지 않다.

<br>

만약 admin 패널에서 users가 어떻게 보여질지를 변경하고 싶다면 users 폴더의 admin.py에 코드를 작성해야 하고, <br>
만약 URLs을 추가하고 싶으면 /config/urls.py 에서 해야 한다.

<br>
