# 接口
---
# 声纹列表

列出当前组里的声纹ID列表

    请求基路径：[服务器IP]:[Port]/v1/
    接口验证ID：appid


### 基本信息
* 请求url：/store/list

* 请求协议：HTTP

* 请求方式：POST

* 请求格式：application/json

* 响应格式：application/json

* 请求参数

| 字段    | 参数位置     | 类型     | 默认值 | 必输项 | 结构 | 描述      |
|-------|----------|--------|-----|-----|----|---------|
| json | body | cust_json |     | 是   |    | <json> |

``` json
    {
          "offset" : 1, //查询起点
          "limit" : 2  //输出数量
    }
```

* 返回参数
``` json
{
    'hasError': False,
    'errorId': '',
    'errorDesc': '',
    'data': {
        'ids': ['09718617-d520-4375-ba32-eafcfd442c48', 'e1a3a60d-263b-4229-88e4-d0c9e1b43036']
    }
}
```

* 返回字段说明
| 字段        | 类型     | 非空 | 结构 | 描述 |
|-----------|--------|----|----|----|
| hasError  | string | 否  |    |    |
| errorId   | string | 否  |    |    |
| errorDesc | string | 否  |    |    |
| data      | object | 否  |    |    |
| ids       | array | 否  |    |  声纹id |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

---

# 声纹查询

根据ID查询声纹信息

    请求基路径：[服务器IP]:[Port]/v1/
    接口验证ID：appid

### 基本信息
* 请求url：/store/vpr

* 请求协议：HTTP

* 请求方式：POST

* 请求格式：application/json

* 响应格式：application/json

* 请求参数

| 字段    | 参数位置     | 类型     | 默认值 | 必输项 | 结构 | 描述      |
|-------|----------|--------|-----|-----|----|---------|
| json | body | cust_json |     | 是   |    | <json> |

``` json
    {
		"id" : "xxxx"
    }
```
* 返回参数
``` json
{
    'hasError': False,
    'errorId': '',
    'errorDesc': '',
    'data': {
        'id': '0d39a539-261d-426d-a4f8-e9f3020cc02d',
        'ctime': '2020-03-25 19:13:07'
    }
}
```
* 返回字段说明
| 字段        | 类型     | 非空 | 结构 | 描述 |
|-----------|--------|----|----|----|
| hasError  | string | 否  |    |    |
| errorId   | string | 否  |    |    |
| errorDesc | string | 否  |    |    |
| data      | object | 否  |    |    |
| topitems  | array | 否  |    |    |
| id        | string | 否  |    | 声纹id  |
| ctime    | string | 否  |    | 创建时间 |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

---

# 删除声纹

删除已注册的声纹，如果没找到则跳过，返回删除数量

    请求基路径：[服务器IP]:[Port]/v1/
    接口验证ID：appid

### 基本信息
* 请求url：/store/remove

* 请求协议：HTTP

* 请求方式：POST

* 请求格式：application/json

* 响应格式：application/json

* 请求参数

| 字段    | 参数位置     | 类型     | 默认值 | 必输项 | 结构 | 描述      |
|-------|----------|--------|-----|-----|----|---------|
| json | body | cust_json |     | 是   |    | <json> |


``` json
    {
		"ids" : [ "id1", "id2", "id3" ]
    }
```
* 返回参数
``` json
{
    'hasError': False,
    'errorId': '',
    'errorDesc': '',
    'data': {
        'count': 2
    }
}
```

* 返回字段说明
| 字段        | 类型     | 非空 | 结构 | 描述 |
|-----------|--------|----|----|----|
| hasError  | string | 否  |    |    |
| errorId   | string | 否  |    |    |
| errorDesc | string | 否  |    |    |
| data      | object | 否  |    |    |
| topitems  | array | 否  |    |    |
| count     | int | 否  |    | 删除的声纹数量  |
