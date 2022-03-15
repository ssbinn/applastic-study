1. secrets.json 파일 만들기 (README.md 파일과 같은 선상에 있도록)

<br>

2. 파일 내에 settings.py에 있는 SECRET_KEY 값 작성
```python
{
  "SECRET_KEY": "[my secret_key]"
}
```

<br>

3. gitignore 파일에 `secrets.json` 파일 추가 <br>
4. settings.py 파일 수정 
```python
import os, json
from django.core.exceptions import ImproperlyConfigured

secret_file = os.path.join(BASE_DIR, 'secrets.json')  # SECRET_KEY 파일 위치

with open(secret_file) as f:
    secrets = json.loads(f.read())

# secrets.json 파일에서 SECRET_KEY 가져오기    
def get_secret(setting, secrets=secrets):
    try:
        return secrets[setting]
    except KeyError:
        error_msg = "Set the {} environment variable".format(setting)
        raise ImproperlyConfigured(error_msg)

SECRET_KEY = get_secret("SECRET_KEY")
```

<br>

### 참고
https://chagokx2.tistory.com/45
