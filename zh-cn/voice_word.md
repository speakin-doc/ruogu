# 接口
---
# 语音转文字（ASR）
输入音频(仅支持16k音频)，返回对应字符串
	
	请求基路径：[服务器IP]:[Port]/v1/
    	接口验证ID：appid


### 基本信息
* 请求url：192.168.0.25:8101/v1/asr/recognize

* 请求协议：HTTP

* 请求方式：POST

* 请求格式：multipart/form-data

* 响应格式：application/json

* 请求参数

| 字段    | 参数位置     | 类型     | 默认值 | 必输项 | 结构 | 描述      |
|-------|----------|--------|-----|-----|----|---------|
| train | formData | file |     | 否  |    | <json> |

* 返回参数
``` json
{
    'hasError': False,
    'errorId': '',
    'errorDesc': '',
    'data': {
        'text': '静夜思李白，床前明月光，疑是地上霜。举头望明月，低头思故乡。',
        'other': ''
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
| text | string | 否  |    | 转换的文字 |
| other  | string | 否  |    | 其他可能参数  |



&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
