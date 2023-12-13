## 增
### 创建文档(指定文档id)

PUT localhost:9200/索引名称/类型名称/文档id

### 创建文档(随机文档id)

POST localhost:9200/索引名称/类型名称 

## 删
### 删除文档

DELETE localhost:9200/索引名称/类型名称/文档id

## 改
### 修改文档

POST localhost:9200/索引名称/类型名称/文档id/_update

## 查
### 查询文档通过文档id

GET localhost:9200/索引名称/类型名称/文档id

### 查询所有文档

POST localhost:9200/索引名称/类型名称/_search