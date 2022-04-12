### Django path

- app_list 페이지에서(all_apps.html) 앱 하나 클릭 시 `url/apps/[앱 id]` 로 가도록 구현할 거야
- **url dispatcher**
    - url에 변수를 가질 수 있게 함
    - 더 알아보기
    - `apps/urls.py > path(”<str:id>, ...”)`
- url tag
    - url/apps/~ 이런 식으로 경로를 기억해야 해 > 그러고 싶지 않아
    - url의 namespace
- url에 엉뚱한 앱 고유 id를 검색했을 때
    - 첫번째 방법
        
        ```python
        if app == None:  # url에 엉뚱한 앱 고유 id를 검색했을 때
                return redirect("/")
        ```
        
    
    - 2번째 방법 - **url reverse**
        
        ```python
        from django.urls import reverse
        
        if app == None:  # url에 엉뚱한 앱 고유 id를 검색했을 때
                return redirect(reverse("core:home"))
        ```
        
        - 가능하다면 url reverse를 사용해야 하는 이유
            - url을 외워 하드코딩하지 않아도 됨
            - url이 변경되어도 url reverse가 변경된 url을 추적하여 누락될 위험을 감소시킨다.
            - urls.py에서 정의한 url pattern의 `name`만 확인하면 view 함수를 통해 매칭되는 url을 찾아 이를 전달받을 수 있다
            
            ![Untitled](https://user-images.githubusercontent.com/83692497/162882052-78e00b1f-6490-49cd-b087-242e5013030e.png)

            
        
    - 3번째 방법 - **404 페이지 (선택)**
        
        ```python
        from django.http import Http404
        
        if app == None:  # url에 엉뚱한 앱 고유 id를 검색했을 때
                raise Http404
        ```
        
        - 브라우저가 404 status를 이해할 수 있고, 방문 기록창에 저장하지 않음
        - error 니까 `return`이 아닌 `raise`
        - raise 하면 장고가 알아서 templates/404.html을 render 함 (단, base.html과 같은 선상에 있어야 함)
