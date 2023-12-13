# 批量更新字段

```json
POST [index]/_update_by_query

{
  "script": {
    "lang": "painless",
    "inline": "if (ctx._source.[abc]== [null]) {ctx._source.[abc]= [0]}"
  }
}
```

当es中数据量非常巨大时，一次请求不能完全执行成功，会出现超时（默认1分钟），此时采用带有搜索条件的批量操作，如下：

```json
POST [index]/_update_by_query

{
  "script": {
    "inline": "ctx._source.[actionTime]=['20181008104853'];ctx._source.[createTime]=['20181008104853']"
  },
  "query": {
    "range": {
      "productID": {
        "gte": 0,
        "lte": 10000
      }
    }
  }

```