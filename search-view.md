### search view

- template, form url setup
    - form을 어떻게 사용하는 지 배우게 됨
    - 일단 검색창을 header에 둘 거고, search는 form인 검색창일 거야
    - user가 엔터를 누르면 form으로 넘어가겠지
    - 우선 앱 이름으로만 검색가능하게 할 거야
    - 앱 이름으로 검색 시 app argument와 함께 /apps/search로 이동했으면 해
    - 앱 이름으로 검색 시 검색창에 검색어가 써져 있으면 해
    - base.html에 block search-bar를 두어서 /apps/search에서 검색창을 숨길 수  있게 됨
