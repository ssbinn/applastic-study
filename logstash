#### 로그스태시 실행
- -e
  ```
  bin/logstash -e 'input { stdin { } } output { stdout { } }'
  ```
- -f : if configurations are set in a file (ex.pipeline.conf)
  ```
  bin/logstash -f pipeline.conf
  ```

#### config.reload.automatic: true
- 원래는 config 파일이 변경되면 로그스태시를 재시작해주어야 하는데, 재시작할 필요가 없도록 config/logstash.yml 에서 `config.reload.automatic: true` 설정
