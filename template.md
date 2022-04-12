### view 작동 방식

브라우저는 내가 방문할 때마다 HTTP Request를 생성함, 그리고 HTTP Response를 응답해줘야 함 

Request로 유저가 로그인 했는지 안했는지 또는 누군가 우리에게 폼을 전송했는지 확인 가능 > 매번 django는 request를 받으면, 그 request을 python object로 변환시켜 줌 > 그리고 모든 view (함수)에 대해서 그 object를 첫번째 argument로 제공해줌

HTTP Response를 반환하지 않아서 오류가 난 경우  > render로 해결 > render(request, template_name, ...) > templates 생성

### template

- context , 내 template에 context는 변수를 보내는 하나의 방법
    - {{변수명}}
- block: 자식 template이 부모 template에게 content를 넘겨주는 창(window)
- 로직을 짤 수 있음
    - {% if %}
    - 주의할 점은 장고 template에서 모든 python 코드가 작동하는 건 아니야 ex. range 안됨, +1 안됨 > {{page.number|add:-1}}
- extends (ex. extends “base.html”)
- apps/all_apps.html 에서 pagination 함수를 호출하지 않고 있음 (ex. previous_page_number)
    - 장고 template에서는 “함수()” 이런 식으로 호출하지 않아도 자동적으로 함수가 호출됨
- urls.py
    - path는 오로지 url과 함수만 갖는다, class 오면 안됨
    
![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0f6a78aa-11e5-4ee6-8bcd-ea677f3161af/Untitled.png)
![Untitled2](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/251c33c2-5067-492d-9e32-51326dd59f4d/Untitled.png)
