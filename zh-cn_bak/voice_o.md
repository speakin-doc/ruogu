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
          "limit" : 2,  //输出数量
          "group" : "test"
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

### 测试用例（python）
```python
import requests
import json

def normal_post(url, data):
    headers = {
        'Content-Type': 'application/json',
        'appid': '此处填入接口验证ID'
    }
    res = requests.post(url, data=json.dumps(data), headers=headers).json()
    return res

def list_vpr(group='ceshi', offset=1, limit=2):
    """获取声纹列表"""
    url_prefix = "http://192.168.0.25:8100/v1/"
    url = url_prefix + 'store/list'
    data = {
        'offset': offset,
        'limit': limit,
        'group': group
    }
    res = normal_post(url, data)
    return res


def main():
    group = 'ceshi'
    offset = 1
    limit = 2
    res = list_vpr(group, offset, limit)
    print(res)


if __name__ == "__main__":
    main()

```

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

### 测试用例（python）

```python
import requests
import json

def read_audio(audio_path):
    """读取音频"""
    with open(audio_path, 'rb') as f:
        audio_content = f.read()
    return audio_content

def get_file_name(file_path):
    """获取文件名"""
    return file_path.split(r'/')[-1]

def register(audio_path, group='ceshi'):
    """声纹注册"""
    url_prefix = "http://192.168.0.25:8100/v1/"
    url = url_prefix + 'vpr/register'
    headers = {
        'appid': '此处填入接口验证ID'
    }
    audio_name = get_file_name(audio_path)
    data = {'group': group}
    files = [('train', (audio_name, read_audio(audio_path)))]
    res = requests.post(url, data=data, files=files, headers=headers).json()
    return res

def normal_post(url, data):
    headers = {
        'Content-Type': 'application/json',
        'appid': '此处填入接口验证ID'
    }
    res = requests.post(url, data=json.dumps(data), headers=headers).json()
    return res

def vpr(audio_id):
    """声纹查询"""
    url_prefix = "http://192.168.0.25:8100/v1/"
    url = url_prefix + 'store/vpr'
    data = {
        'id': audio_id
    }
    res = normal_post(url, data)
    return res


def main():
    audio_path = 'audio/2.wav'
    register_res = register(audio_path)
    audio_id = register_res.get('data').get('id')
    res = vpr(audio_id)
    print(res)


if __name__ == "__main__":
    main()
```
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

### 测试用例（python）

```python
import requests
import json

def get_file_name(file_path):
    """获取文件名"""
    return file_path.split(r'/')[-1]

def register(audio_path, group='ceshi'):
    """声纹注册"""
    url_prefix = "http://192.168.0.25:8100/v1/"
    url = url_prefix + 'vpr/register'
    headers = {
        'appid': '此处填入接口验证ID'
    }
    audio_name = get_file_name(audio_path)
    data = {'group': group}
    files = [('train', (audio_name, read_audio(audio_path)))]
    res = requests.post(url, data=data, files=files, headers=headers).json()
    return res

def normal_post(url, data):
    headers = {
        'Content-Type': 'application/json',
        'appid': '此处填入接口验证ID'
    }
    res = requests.post(url, data=json.dumps(data), headers=headers).json()
    return res

def remove(ids):
    """删除声纹"""
    url_prefix = "http://192.168.0.25:8100/v1/"
    url = url_prefix + 'store/remove'
    data = {
        'ids': ids
    }
    res = normal_post(url, data)
    return res


def main():
    audio_paths = ['audio/2.wav', 'audio/3.wav']
    audio_ids = []
    for audio_path in audio_paths:
        register_res = register(audio_path)
        audio_id = register_res.get('data').get('id')
        audio_ids.append(audio_id)
    res = remove(audio_ids)
    print(res)


if __name__ == "__main__":
    main()
```

---

