#### text, keyword 매핑 처리
text 타입은 입력된 문자열을 inverted index 구조로 만들고, keyword 타입은 입력된 문자열을 하나의 토큰으로 저장함 

- text + keyword

'William'이라고 검색을 할 때도 검색이 되어야 하고, 'William Shakespeare'라는 작가의 작품만 따로 집계를 하고 싶을 수 있음
검색과 집계가 가능하도록 text와 keyword를 같이 저장
```
ex. "author': "William Shakespeare"
``` 

- text

'Romeo and Juliet'만으로 집계를 할 일은 없지만, 'Romeo'나 'Juliet'으로 검색을 하는 일은 있을테니까 text 타입으로 저장 
```
ex. "title": "Romeo and Juliet"
```


- keyword

집계만 할 가능성이 있고, 검색을 할 때도 "US" 같이 딱 찝어서 검색을 하니까 keyword 타입으로 저장
```
"contry_code": {
    "type": "keyword"
}
```

