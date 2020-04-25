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

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
