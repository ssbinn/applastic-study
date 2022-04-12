```python
def genre_API():  # 장르명 추출 함수
    es = Elasticsearch(
        cloud_id="[Cloud ID]",
        http_auth=("[user]", "[password]"),
    )
    index = es.search(index="[index name]")
    size = index["hits"]["total"]

    resp = es.search(
        index="[index name]",
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
