- update 관련
[https://blog.indexall.net/2017/04/logstash-jdbc-update-delete.html](https://blog.indexall.net/2017/04/logstash-jdbc-update-delete.html)

[https://discuss.elastic.co/t/logstash-adding-duplicate-rows-for-every-run/44775](https://discuss.elastic.co/t/logstash-adding-duplicate-rows-for-every-run/44775)

document_id를 지정해주지 않으면, logstash를 실행할 때 문서에 새로운 document_id가 랜덤으로 부여되며 문서가 추가됩니다. 

document_id를 고정으로 설정하면 새로 추가되지 않고, 덮어 씌게 되어 중복된 파일이 생성되지 않습니다.

**우리 프로젝트는 어플의 히스토리가 중요하게 작용하기 때문에 이 방법을 사용하지 않았다는 것도 언급하기**

문제 : 로그스태시 output에 document_id => "trackId"를 추가하면 문제가 해결
```
input {
    file {
        path => ["/Users/kyj/Desktop/elastic/exrawdata/kr/iphone/*/*.json"]
        codec => "json" 
    }
}

output {
    elasticsearch {
        hosts => ["34.64.163.90:9200"]
        index => "test-apple-0323-%{[ChartDevice]}-%{[ChartCountry]}-%{[ChartName]}-%{[ChartField]}"
        # index => "test-%{ChartField}"
        # index => "test-please"
        user => "app"
        password => "elastic"
    }
}
```
