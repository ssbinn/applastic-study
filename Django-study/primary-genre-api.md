```python
def genre_API():  # 장르명 추출 함수
    es = Elasticsearch("http://34.64.163.90:9200", basic_auth=("kyj", "210is1024"))
    index = es.search(index="chart-apple-iphone-kr-topfree-6005")
    size = index["hits"]["total"]

    resp = es.search(
        index="chart-apple-iphone-kr-topfree-6005",
        body={"size": size["value"], "query": {"match_all": {}}},
    )

    list = []
    result = []
    i = 1
    while i < size["value"]:
        list = resp["hits"]["hits"][i]["_source"]["genres"]
        for j in list:
            if j not in result:  # 중복제거
                result.append(j)
        i += 1

    return result
```
