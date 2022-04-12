### Pagination

- 컨벤션
    - 가장 많이 쓰는 방법
    - ex. url 뒤에 page=1 붙이는 거
- 블로그 정리하기
    - 주먹구구식으로 구현하는 방법
    - applastic 프로젝트에서는 app list 보여주는 페이지에서만 paginator가 필요해서 장고의 paginator를 사용했다는 것을 먼저 설명
    - 후에 다른 애플리케이션 (ex.리뷰)에서도 동일한 paginator를 구현해야 하는 일이 없도록 하는 방법 (?)
- page 예외 처리 - python
    - paginator는 page object를 반환하는 두개의 메소드를 가짐 > `get_page`와 `page`
        - `get_page` 는 만약 페이지 넘버가 음수이거나 총 페이지 숫자보다 크다면 마지막 페이지를 반환함
        - `page` 는 get_page 보다 컨트롤 해야 할 게 많음 (ex. 첫 페이지 넘버 1로 설정하는 일 등), 총 페이지 숫자보다 크면 emptypage 에러를 보임
        - 예외 처리를 위해 `page`를 사용함
- orphans
    - 399 페이지에 있는 3개의(index에 따라 달라짐) 요소만 있음 > orphan(고아) 처리 > orphans는 요소의 목록 > `orphans=5` 설정 > 요소가 6개, 7개 등이 있다면 마지막 페이지에 남기고, 3개 정도 있다면 마지막 전 페이지에 13개의 요소를 보여줌
    

### ~~function vs class based view~~

- ~~ListView~~
- ~~개념 정리~~
- ~~다른 프로젝트에서 다뤄보기~~
