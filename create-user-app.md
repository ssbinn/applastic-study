<br>

### Replacing Default User 
장고는 이미 user 애플리케이션을 갖고 있어, 부족하진 않지만 확장할 필요가 있다면 확장 가능하다. <br>
username, 유효성 검사, 성, 이름, 이메일 필드들 등이 제공되는데, 여기에 프로필 사진을 설정하거나 생년월일, 언어 등 확장 기능을 추가할 수 있다.

<br>

장고에서 디폴트 user 모델을 덮어쓰려면, 내가 만든 user 애플리케이션을 config/settings.py 에서 설치해야 한다. [참고] (https://docs.djangoproject.com/en/2.2/topics/auth/customizing/) <br>
db.sqlite3 파일 삭제 후 config/settings.py에서 `AUTH_USER_MODEL = "users.User" 추가 > makemigration > 서버 재가동`

<br>

makemigration까지 마치고 서버를 재가동시켰을 때 더이상 에러가 나오지 않지만, /admin 주소로 접속했을 때 user가 보이지 않음 <br>
**User 모델을 user/admin.py와 연결**해서 해결해야 한다. <br>

<br>

#### docstring
파이썬에서 쓰는 표준 형식, 클래스를 만들 때마다 무슨 클래스인지 명시할 때 쓰인다.

<br>

#### models.ImageField() 에러
user 모델을 디자인하는 중에 `models.ImageField()` 때문에 에러가 나왔다. <br>
pillow 설치 안하면 image 필드를 사용할 수 없다고 함, pillow는 이미지를 처리하는 파이썬 라이브러리, pip로 설치하라는 문구가 뜨지만 pipenv를 사용해서 설치해야 한다. 

<br>

### 정리
우리가 장고를 사용하는 게 아니라 장고가 우리 코드를 사용하는 것이다. <br>
장고는 **장고 ORM(object relational mapping)** 을 탑재하고 있는데, 이게 내 파이썬 코드를 SQL 문으로 바꿔서 데이터베이스가 알아들을 수 있게 만든다. <br>
models.py에 집어넣는 모든 걸 장고가 알아서 데이터베이스 테이블로 만들어준다는 얘기 

<br>

Model은 fields로 이루어져 있다. char 필드, date 필드, image 필드... <br>
image 필드의 경우 이미지 파일만 선택 가능한데, 이는 장고가 데이터 유효성 검사까지 해준다는 얘기이기도 하다.

<br>

Model을 직접 보려면 admin 패널에서 볼 수 있었어, admin.py에서 admin 패널의 구성을 바꿀 수 있었고, admin.py에서 Model을 가져오려면 register를 해줘야 하고, register 하기 위해선 class가 필요해. 그 class는 기본적으로 Model을 조정할 수 있어 <br> 
그리고 장고가 내가 만든 폴더를 인식하도록 하려면 setting.py에 등록해줘야 한다. <br>
장고가 원래 갖고 있는 User가 아닌 내가 만든 User를 쓰려고 `AUTH_USER_MODEL`를 바꿔줬었어 

<br>

다음으로 넘어가기 전에 데이터베이스 삭제하고, pycache 폴더가 있다면 그것도 삭제하고, migration도 삭제하자 (이유는 다음에 추가)
