# 接口声明
---
# 声纹注册
导入音频声纹注册入库，返回声纹ID.

    请求基路径：[服务器IP]:[Port]/v1/
    接口验证ID：appid

### 基本信息
* 请求url：vpr/register

* 请求协议：HTTP

* 请求方式：POST

* 请求格式：multipart/form-data

* 响应格式：application/json


* 请求参数

| 字段    | 参数位置     | 类型     | 默认值 | 必输项 | 结构 | 描述      |
|-------|----------|--------|-----|-----|----|---------|
| train | formData | file   |     | 是   |    |  待注册音频(该字段可以有一个或多个） |
| train | formData | file   |     | 否   |    |  待注册音频     |

* 返回参数
``` json
{
    'hasError': False,
    'errorId': '',
    'errorDesc': '',
    'data': {'id': '25526fd1-7053-4c65-b94e-09d71b079ef9'  
}  
```
* 返回字段说明
| 字段       | 类型     | 非空 | 结构 | 描述 |
|-----------|--------|----|----|----|
| hasError  | string | 否  |    |  是否请求请求成功  |
| errorId   | string | 否  |    |  错误码  |
| errorDesc | string | 否  |    |  错误描述  |
| data      | object | 否  |    |  返回声纹ID  |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

---


# 音频比对1:1

音频文件1:1比对，返回声纹对比分数.

    请求基路径：[服务器IP]:[Port]/v1/
    接口验证ID：appid

### 基本信息
* 请求url：/vpr/compare

* 请求协议：HTTP

* 请求方式：POST

* 请求格式：multipart/form-data

* 响应格式：application/json

* 请求参数

| 字段    | 参数位置     | 类型   | 默认值 | 必输项 | 结构 | 描述 |
|-------|----------|------|-----|-----|----|----|
| train | formData | file |     | 是   |    |    |
| test  | formData | file |     | 是   |    |    |

* 返回参数
``` json
{
    'hasError': False,
    'errorId': '',
    'errorDesc': '',
    'data': {'score': -16.13147}
}  
```

* 返回字段说明
| 字段        | 类型     | 非空 | 结构 | 描述   |
|-----------|--------|----|----|------|
| hasError  | string | 否  |    | 是否请求请求成功  |
| errorId   | string | 否  |    |  错误码  |
| errorDesc | string | 否  |    | 错误描述 |
| data      | object | 否  |    |  比对分数 |


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

---

# 音频比对1:n

音频1:n比对，返回对比分数队列.

    请求基路径：http://[服务器IP]:[Port]/v1
    接口验证ID：appid

### 基本信息
* 请求url：/vpr/compare_n

* 请求协议：HTTP

* 请求方式：POST

* 请求格式：multipart/form-data

* 响应格式：application/json

* 请求参数

| 字段    | 参数位置     | 类型     | 默认值 | 必输项 | 结构 | 描述      |
|-------|----------|--------|-----|-----|----|---------|
| train | formData | file |     | 是   |    | train为用于训练的音频文件，只能有一个 |
| test | formData | file |     | 是   |    | test是用于测试的音频文件，，可以有若干个 |
| test | formData | file |     | 否   |    |    |
| test | formData | file |     | 否   |    |    |

* 返回参数
``` json
{
    'hasError': False,
    'errorId': '', 
    'errorDesc': '', 
    'data': {
        'cmpitems': [
            {
                'filename': '2.wav', 
                'score': 132.01208
            }, {
                'filename': '3.wav', 
                'score': 122.239685
            }, {
                'filename': '4.wav', 
                'score': 134.79205
            }, {
                'filename': '5.wav', 
                'score': 134.0712
            }
        ]
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
| cmpitems | array | 否  |    |    |
| filename | string | 否  |    | 比对音频文件名 |
| score | double | 否  |    |  比对分数  |


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

---

# 声纹比对1:1
注册声纹返回声纹ID，根据ID进行1:1对比，返回对比分数

    请求基路径：[服务器IP]:[Port]/v1/
    接口验证ID：appid

### 基本信息
* 请求url：/vpr/compare_by_id

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
    "train" : "xxx",
    "test" : "xxx"
}
```


* 返回参数

``` json
{
    'hasError': False, 
    'errorId': '', 
    'errorDesc': '', 
    'data': {'score': 132.01208}
}
```

* 返回字段说明

| 字段        | 类型     | 非空 | 结构 | 描述 |
|-----------|--------|----|----|----|
| hasError  | string | 否  |    |    |
| errorId   | string | 否  |    |    |
| errorDesc | string | 否  |    |    |
| data      | object | 否  |    |    |
| score     | double | 否  |    | 比对分数 |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

---

# 声纹比对1:n
注册声纹返回声纹ID，根据ID进行1:n对比，返回对比分数

    请求基路径：[服务器IP]:[Port]/v1/
    接口验证ID：appid

### 基本信息
* 请求url：/vpr/compare_by_id_n

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
    "train" : "24e794f1-cd46-4d80-8131-26df86099507",
    "test_ids" : [ "24e794f1-cd46-4d80-8131-26df86099507", "24e794f1-cd46-4d80-8131-26df86099507", "24e794f1-cd46-4d80-8131-26df86099507" ]
}
```

* 返回参数
``` json
{
    'hasError': False, 
    'errorId': '', 
    'errorDesc': '', 
    'data': {
        'cmpitems': [
            {
                'id': '34ee8b58-a5e1-49dd-bd1d-e92c859e97c7', 
                'score': 162.62918
            }, {
                'id': '434edf49-5bdf-469c-b06b-71c4e58432c3', 
                'score': 132.01208}
        ]
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
| cmpitems  | array  | 否  |    |    |
| id        | string | 否  |    | 比对的声纹id |
| score     | double | 否  |    | 比对分数 |


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

---

# 音频-声纹比对1:1
音频和注册过的声纹进行1:1对比，返回对比分数

    请求基路径：[服务器IP]:[Port]/v1/
    接口验证ID：appid

### 基本信息
* 请求url：/vpr/compare_with_id

* 请求协议：HTTP

* 请求方式：POST

* 请求格式：multipart/form-data

* 响应格式：application/json

* 请求参数

| 字段    | 参数位置     | 类型     | 默认值 | 必输项 | 结构 | 描述      |
|-------|----------|--------|-----|-----|----|---------|
| train | formData | file   |     | 是   |    |         |
| test | formData | string |     | 是   |    | 对音频的声纹id |

* 返回参数
``` json
{
    'hasError': False, 
    'errorId': '', 
    'errorDesc': '', 
    'data': {
        'id': 'af18a3be-49a3-49ce-8726-a3eb0466d023', 
        'score': 132.01208
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
| id        | string | 否  |    | 比对的声纹id |
| score     | double | 否  |    | 比对分数 |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

---
# 音频-声纹比对1:n
音频和注册过的声纹进行1:n对比，返回对比分数

    请求基路径：[服务器IP]:[Port]/v1/
    接口验证ID：appid

### 基本信息
* 请求url：/vpr/compare_with_id_n

* 请求协议：HTTP

* 请求方式：POST

* 请求格式：multipart/form-data

* 响应格式：application/json

* 请求参数

| 字段    | 参数位置     | 类型     | 默认值 | 必输项 | 结构 | 描述      |
|-------|----------|--------|-----|-----|----|---------|
| train | formData | file   |     | 是   |    |         |
| test_ids | formData | string   |     | 是   |    |   要比对的声纹id，可以有若干个    |

* 返回参数
``` json
{
    'hasError': False, 
    'errorId': '', 'errorDesc': '', 
    'data': {
        'cmpitems': [{
            'id': 'd3757eef-0006-4f09-a2a9-61f30b432177', 
            'score': 132.01208
            }, {
            'id': 'feab3ba5-d75e-4256-a4eb-25779b32179b', 
            'score': 122.239685
            }
        ]
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
| cmpitems  | string | 否  |    |    |
| id        | string | 否  |    | 声纹id |
| score     | double | 否  |    |  比对分数 |


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

---

# 音频Topn

一份音频文件和一组音频文件对比，输出比分最高的前n项

    请求基路径：[服务器IP]:[Port]/v1/
    接口验证ID：appid

### 基本信息
* 请求url：/vpr/top

* 请求协议：HTTP

* 请求方式：POST

* 请求格式：multipart/form-data

* 响应格式：application/json 

* 请求参数

| 字段    | 参数位置     | 类型     | 默认值 | 必输项 | 结构 | 描述      |
|-------|----------|--------|-----|-----|----|---------|
| train | formData | file   |     | 是   |    |         |
| n | formData | int  |     | 是   |    | 匹配前n项，要小于 APP 限定值  |

* 返回参数
``` json
{
    'hasError': False,
    'errorId': '',
    'errorDesc': '',
    'data': {
        'topitems': [{
            'id': '5a68142a-00e8-4b52-90f3-93db70e9f733',
            'score': 162.62918
        }, {
            'id': '9f3cae11-7464-4634-9314-895f3122f6ce',
            'score': 162.62918
        }, {
            'id': '25526fd1-7053-4c65-b94e-09d71b079ef9',
            'score': 162.62918
        }]
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
| score     | double | 否  |    | 比对分数 |


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

---
# 声纹Topn

    一份注册过的声纹和一组注册过的声纹进行音素对比，返回比分最高的前n项
    
    请求基路径：[服务器IP]:[Port]/v1/
    接口验证ID：appid

### 基本信息
* 请求url：/vpr/top_by_id


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
    "train" : "xxx",
    "n" : 3,
}

```
* 返回参数
``` json
{
    'hasError': False,
    'errorId': '',
    'errorDesc': '',
    'data': {
        'topitems': [{
            'id': '7aff64fc-cb64-42e9-8e78-db7ac9e78f8a',
            'score': 162.62918
        }, {
            'id': 'c7dc60a1-0a0e-431f-9ef2-a6deb2d14555',
            'score': 162.62918
        }]
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
| score     | double | 否  |    | 比对分数 |

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

---
