# 接口
# 语种识别

* 语种识别：
支持中，日，韩，俄，法，西，阿拉伯语，孟加拉语，布列塔尼语，加泰罗尼亚语，楚瓦什语，迪维希语，荷兰语，英语，爱沙尼亚语，巴斯克语，波斯语，德语，粤语，哈卡钦语等40种语言的语种识别。

    请求基路径：[服务器IP]:[Port]/v1/
    接口验证ID：appid

### 基本信息
* 请求url：/language/check

* 请求协议：HTTP

* 请求方式：POST

* 请求格式：multipart/form-data

* 响应格式：application/json

* 请求参数

| 字段    | 参数位置     | 类型     | 默认值 | 必输项 | 结构 | 描述      |
|-------|----------|--------|-----|-----|----|---------|
| train | formData | file |     | 是   |    |   |

* 返回参数
``` json
{
	'hasError': False,
	'errorId': '',
	'errorDesc': '',
	'data': {
		'type': '阿拉伯语'
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
| type  | string | 否  |    |  语种类型如（普通话、英语  |

### 测试用例（python）

```python
import requests
import json

def language(train_audio_path):
    """语种识别"""
    headers = {'appid': '接口验证ID'}
    url = "http://192.168.0.25:8100/v1/language/check"
    train_audio_name = get_file_name(train_audio_path)
    files = [
        ('train', (train_audio_name, read_audio(train_audio_path)))
    ]
    res = requests.post(url, files, headers).json()
    return res


def main():
    train_audio_path = 'audio/Arabic_xfss_B.wav'
    res = language(train_audio_path)
    print(res)


if __name__ == "__main__":
	main()
```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

---
# 防攻击检测

    请求基路径：[服务器IP]:[Port]/v1/
    接口验证ID：appid

### 基本信息
* 请求url：/anti_attack/varify

* 请求协议：HTTP

* 请求方式：POST

* 请求格式：multipart/form-data

* 响应格式：application/json

* 请求参数

| 字段    | 参数位置     | 类型     | 默认值 | 必输项 | 结构 | 描述      |
|-------|----------|--------|-----|-----|----|---------|
| train | formData | file |     | 是   |    |   |

* 返回参数
``` json
{
	'hasError': False,
	'errorId': '',
	'errorDesc': '',
	'data': {
		'split': False,
		'spoof': False,
		'tts': True
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
| split  | boolean | 否  |    |  是否拼接  |
| spoof  | boolean | 否  |    |  是否伪造  |
| tts  | boolean | 否  |    |  是否合成  |

### 测试用例（python）

```python
import requests
import json

def anti_attack(train_audio_path, group='ceshi'):
    """防合成攻击"""
    headers = {'appid': '接口验证ID'}
    url = "http://192.168.0.25:8100/v1/anti_attack/varify"
    train_audio_name = get_file_name(train_audio_path)
    # train_audio_name = self.get_file_name(r'./audio/wmv.wmv')
    data = {'group': group}
    files = [
        ('train', (train_audio_name, read_audio(train_audio_path)))
    ]
    res = requests.post(url, data, files, headers).json()
    return res

def main():
    train_audio_path = 'audio/防合成攻击.wav'
    res = anti_attack(train_audio_path)
    print(res)


if __name__ == "__main__":
	main()

```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

---
# 性别识别

    请求基路径：[服务器IP]:[Port]/v1/
    接口验证ID：appid

### 基本信息
* 请求url：/gender/check

* 请求协议：HTTP

* 请求方式：POST

* 请求格式：multipart/form-data

* 响应格式：application/json

* 请求参数

| 字段    | 参数位置     | 类型     | 默认值 | 必输项 | 结构 | 描述      |
|-------|----------|--------|-----|-----|----|---------|
| train | formData | file |     | 是   |    |   |

* 返回参数
``` json
{
	'hasError': False,
	'errorId': '',
	'errorDesc': '',
	'data': {
		'sex': '女'
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
| sex  | string | 否  |    |  男或女  |

### 测试用例（python）
```python
import requests
import json
def gender(train_audio_path, group='yaocheng'):
    """性别识别"""
    headers = {'appid': '接口验证ID'}
    url = 'http://192.168.0.25:8100/v1/gender/check'
    train_audio_name = get_file_name(train_audio_path)
    data = {'group': group}
    files = [
        ('train', (train_audio_name, read_audio(train_audio_path)))
    ]
    res = requests.post(url, data, files, headers).json()
    return res


def main():
    train_audio_path = 'audio/小薇_1.wav'
    res = gender(train_audio_path)
    print(res)


if __name__ == "__main__":
	main()
```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
