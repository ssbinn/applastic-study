- 윈도우 기준
- 파이썬 버전 `3.9.10`
- 장고 버전 `2.2.5`

<br>

**장고를 선택한 이유**는 웹 사이트와 사용자 간의 상호작용이 많지 않고, 콘텐츠 위주의 페이지를 만들 예정인데, 장고가 그런 유형의 사이트를 만들기 적합하다고 생각하기 때문 <br>
클릭 시 즉시 반응하고, 페이지 새로고침 없이 팝업을 띄우는 등 사용자 간 많은 상호작용이 이루어지는 사이트를 구상중이라면 리액트를 이용 했을 것

그렇다고 장고 템플릿으로 대화형 웹 사이트를 만들 수 없다는 얘기는 아니야

<br>

## 내 로컬에서 장고 환경세팅

### pipenv 설치 
`pip install Django` 로 장고를 설치하는 걸 권장하지 않는 이유 > pip는 모든 걸 전역으로 설치하기 때문 <br>
그래서 pipenv를 설치해야 하고, pipfile이라는 걸 생성할텐데, 이걸 쓰면 django를 해당 프로젝트 환경에만 설치할 수 있게 됨 (npm에 있는 package.json 처럼!) <br>
pipenv는 버블을 생성하는 것과 같음, 버블에다가 패키지를 설치하게 되니까 전역으로 설치되지 않도록 해준다.

<br>

`pip install --user pipenv`  (cmd) <br>
콘솔에서 `pipenv` 치면 가이드라인이 나온다면 성공.

<br>

만약 나오지 않는다면 pip list 에서 virtualenv 이 설치되어있는지 확인하고, <br>
`pip uninstall virtualenv`  <br>
`pip uninstall pipenv`  <br>
`pip install pipenv` 

<br>

### 독립된 개발 환경 만들기

원하는 곳에 폴더를 생성하고, <br>
그 폴더 안에서 pipenv를 써서 독립된 개발 환경(버블)을 만들 거야 <br>
pipenv에게 3.9 버전을 기반으로 하는 환경을 만들어달라고 알려야 함 <br>
장고는 파이썬 3에서 잘 동작하기 때문에 **pipenv 공식 페이지**에서 지원하는 파이썬 버전을 확인하고 아래를 따라하자 

<br>

`pipenv --three` <br>
`code .`  :  폴더를 vscode에서 확인 <br>
Pipfile은 package.json 이랑 같은 것임 <br>
이제 터미널에서 생성한 가상환경의 내부로 들어가기 위해 vscode 내 터미널에서 `pipenv shell` 실행 <br>
이제 버블 안에 들어왔으니 여기서 django를 설치할 거야

<br>

만약 최신 버전의 장고를 다운받고 싶다면 [장고 설치 가이드](https://www.djangoproject.com/download/)를 참고하자 <br>
터미널에서 `pipenv install Django==2.2.5` ( **pip 아닌 거 주의** ) <br>
버블에 잘 설치된 건지 확인하기 위해 `django-admin` 

<br>

pipenv shell 이 아닌 다른 shell (예를 들어 새 터미널을 열면 나오는 powershell같은)에서 `django-admin` 하면 원하지 않는 결과가 나올텐데, 그게 버블 바깥과 버블 내부의 차이 <br>
주의해야 할 점은 이 프로젝트에서 django로 뭔가를 하려면 어떤 콘솔을 쓰던 간에 `pipenv shell`을 먼저 실행해야 하고, `django-admin`으로 잘 작동하는 지 확인해야 함

<br>

### 깃허브 연동
깃허브에서 레파지토리 생성 <br>
주의할 점은 vscode에서 작업 파일(버블) 내에서 아래의 코드를 따라쳐선 안됨 <br>
`git init` <br>
`git remote add origin [레파지토리 주소]` <br>
`git add .` <br>
`git commit -m "[커밋 메시지]"` 

<br>

`README.md` `.gitignore` 만들고, (gitignore은 깃헙에 올릴 필요가 없는 파일이나 보안문제로 공개되면 안되는 정보 등을 위한 것) <br>
구글에 `gitignore python`검색 <br>
디폴트로 쓰이는 gitignore를 찾을 수 있음 <br>
복붙한 뒤 commit 

<br>

### creat django project

생성한 폴더안에서 `django-admin startproject config` <br>
그러면 config 폴더가 생성되는데, 폴더의 이름을 `Aconfig`로 변경, 안에 있는 config 폴더와 manage.py 파일을 밖으로 꺼내기 위함, 옮긴 뒤에 Aconfig 폴더는 삭제 <br>
주의할 점은 vscode에서 `ctrl+shift+p` 단축키를 누르면 python interpreter를 선택할 수 있는데, pipenv가 붙어있는 버전을 선택해야 함 <br>
가상환경에 설정된 파이썬 버전으로 작업하기 위함

<br>

### vscode 개발환경 세팅 

컴파일 언어는 컴파일러가 프로그램 시작 전 에러를 잡아내줌 <br>
파이썬은 컴파일 언어가 아니고 runtime 언어기 때문에, 프로그램 실행시킨 뒤 사소한 에러가 발생하는 걸 방지하기 위해 Linter 라는 걸 마련함 

<br>

Linter는 기본적으로 내가 쓴 코드를 보면서 에러가 생길 부분을 미리 감지하려고 하고, 파이썬 가이드라인을 따를 수 있도록 도와줌 <br>
사용할 Linter는 `flake8` <br>
`ctrl+shift+p` 단축키에서 select linter 클릭 후 `flake8` 선택 <br>
설치되지 않았다면 설치하기  

<br>

Formatter는 코드를 더 보기좋게 수정해줌 <br>
설치할 formatter는 `black` <br>
(저장할 때마다 하단에 formatting with black이 뜸) 

<br>

설치를 마치면, <br>
config/settings.py에 에러를 Linter가 잡아줌, 라인의 길이가 79자를 넘어서 에러라고 판단하는데 이건 예전 컴퓨터의 스크린이 작아서 설정해둔 숫자라서 Linter의 설정을 수정해줘야 함 <br>
`ctrl+shift+p > Preferences: Open Settings (JSON) 클릭` <br>
vscode settings.json 파일에서 `"python.linting.flake8Args": ["--max-line-length==88"]` 코드 추가 

<br>

### 내 로컬 서버 외부 접속 허용하기
[장고 공식 문서 참고](https://docs.djangoproject.com/en/2.1/ref/django-admin/#django-admin-runserver) <br>
기본 IP 주소인 `127.0.0.1`은 다른 사람이 접속을 못해, localhost로 접속하는 거랑 똑같아  <br>
그래서 네트워크의 다른 시스템에서 개발 서버를 볼 수 있도록 하려면 자체 IP 주소(예: `192.168.2.1`) 또는 `0.0.0.0`( `::`IPv6이 활성화된 상태에서)를 사용해야 함

<br>

장고 settings.py 에서 `ALLOWED_HOST = [내 (사설)IP주소]` 코드 추가 후에 <br>
`python manage.py runserver [내 ip 주소]:8000`
