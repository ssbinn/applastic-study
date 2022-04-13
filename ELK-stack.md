### GCP VM 인스턴스로 실습환경 만들기

#### 방화벽 생성
- [VPC 네트워크] - [방화벽] - [방화벽 규칙만들기] : [대상 태그] 지정 (lab) - [소스 범위] 0.0.0.0/0 - [프로토콜 및 포트] 모두허용

#### VM 인스턴스 생성
- [VM 인스턴스] - [인스턴스 만들기] : 서울 - centos로 변경- [방화벽] 네트워킹 - [네트워크 태그]에 방화벽 대상 태그 지정했던 태그 명 적기 (lab)

#### 윈도우 - putty 설치
- 설치 후 [putty gen] 에서 ssh 키 받기
putty에 (GCP VM인스턴스 외부 IP 복사), (프라이머리 키 저장한 파일 등록) - [open] - ssh 키에서 사용자 이름 입력

#### GCP에 ssh key 등록
- [Compute Engine] - [메타데이터] - [SSH 키]

#### putty 기본설정
- 루트 패스워드 설정
```
sudo passwd
```

- 기본 프로그램 설치
```
sudo yum install y wget
```

--- 

### 엘라스틱 설치
- 다운로드 ( 압축 푸는 명령어: tar -xzf )
```
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.17.0-linux-x86_64.tar.gz
```

- 정상 실행 여부 체크 
json 형태로 출력된다면 제대로 실행된 것 (putty - [Duplicate Session])
```
curl http://localhost:9200
```

- elasticsearch.yml
```
cluster.name: lab
node.name: node-1
network.host: 0.0.0.0
xpack.security.enabled: true
```

### 키바나 설치
- 다운로드 ( 압축 푸는 명령어: tar -xzf )
```
wget https://artifacts.elastic.co/downloads/kibana/kibana-7.17.0-linux-x86_64.tar.gz
```

- kibana.yml
```
server.port: 5601
server.host: "0.0.0.0"
elasticsearch.hosts: ["http://localhost:9200"]
elasticsearch.username: "[username]" 
elasticsearch.password: "[password]"
```

#### elasticsearch, kibana 백그라운드 실행
```
./bin/elasticsearch -d -p pid

./bin/kibana> /dev/null 2>&1
```

#### elasticsearch, kibana 중지
```shell
# Elasticseasrch pid 확인
ps -ef | grep elasticsearch
kill -9 [pid]

# Kibana pid 확인
ps -ef | grep node
kill -9 [pid]
```

---
### FileBeat 

#### FileBeat 설치
- 다운로드 ( 압축 푸는 명령어: tar -xzf )
```
wget https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.17.0-linux-x86_64.tar.gz
```

- filebeat 구동 (엘라스틱에 데이터 넣기)
```
./filebeat -e
```

--- 

### Logstash 

#### Logstash 설치
- 다운로드 ( 압축 푸는 명령어: tar -xzf )
```
wget https://artifacts.elastic.co/downloads/logstash/logstash-7.17.0-linux-x86_64.tar.gz
```

- lohstash 구동
```
./bin/logstash -f pipeline/lab.conf
```
