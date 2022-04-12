### TailwindCSS

- class name 자동완성 기능을 위해 vscode 내에서 `Tailwind CSS IntelliSense` 설치
- 폴더 경로 터미널 내에서
    - (물론 이걸 위해선 node.js 와 gulp 12.13.0버전이 설치되어 있어야 해 > gulp는 아래에서  설치하는 데 무슨 말인지 모르겠지만 일단 그래)
    - `npm init`
    - package.json 파일 수정 (깃허브 applastic-django 참고)
    - `npm i gulp gulp-postcss gulp-sass gulp-csso node-sass -D`
    - `npm install tailwindcss -D`
    - `npm i autoprefixer -D`
    - 생성된 node_modules을 커밋하지 않기 위해 .gitignore에 `node_modules/` 추가
    - `npx tailwind init`
- [manage.py](http://manage.py) 와 같은 선상에 `gulpfile.js` 파일, `assets` 폴더 추가
    - assets 폴더 안에 모든 scss 파일을 넣을 거야, gulp 전에 하는 거고 나중에 모든 걸 static 폴더 안에 넣을 거야
- `npm i` > `npm run css` 으로 실행
    - scss 파일을 변경했을 때, apply를 사용할 때는 항상 `npm run css` 으로 변경 결과 확인
    - HTML 파일로 css 작업을 할 땐 매번 `npm run css` 할 필요 없음
- 자동으로 `static/css/styles.css` 생성됨
    - `gulp-sass` 오류
    
    ```bash
    Error in plugin "gulp-sass"
    Message:
    
    gulp-sass no longer has a default Sass compiler; 
    please set one yourself.
    Both the "sass" and "node-sass" packages are permitted.
    For example, in your gulpfile:
    
      const sass = require('gulp-sass')(require('sass'));
    
    [18:45:58] The following tasks did not complete: default
    [18:45:58] Did you forget to signal async completion?
    ```
    
    - 해결
        - `npm i --save-dev sass`
        - gulpfile.js 파일 내에서 `const sass = require("gulp-sass");` > `const sass = require("gulp-sass")(require("sass"));` 코드 변경
- static 폴더가 expose 될 수 있도록 [settings.py](http://settings.py) 에서
    
    ```python
    STATIC_URL = "/static/"
    
    STATICFILES_DIRS = [os.path.join(BASE_DIR, "static")]
    ```
    
- base.html 에

```python
{% load static %}
...
<head>
...
<link rel="stylesheet" href="{% static 'css/styles.css' %}"> 추가
```
