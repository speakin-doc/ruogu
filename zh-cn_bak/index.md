# 概述
# 平台简介

国音智能若谷开发平台，依靠自主研发的声学模型和语言模型，提供全栈式语音服务，含声纹识别、语种识别、性别识别、防攻击检测以及语音转写识别服务，若谷开放平台提供私有化接口授权和开发文档，致力于为开发者提供一站式语音定制服务。

# 服务协议
开发者一经注册或使用本协议下任何服务即视为对本协议条款的理解和接受，开发者违反本协议时国音智能有权按其违反情况限制或停止向开发者提供语音服务，并有权追究开发者的相关责任。


# 常见问题
* 参数格式错误： 该错误表示传入参数格式不对，如需要一个int数据，但是传入了字符串
* 参数逻辑错误：该错误表示传入参数逻辑错误，如待传入的一个int数据最大为200，但是传入了超过200
* 没有上传文件或者文件数量不对
* 音频文件大小有问题
* 服务器错误
* 认证失败，没有访问权限（请传入正确的 appid）

# appid（必须）
请求头处添加,通过appid的形式进行接口调用权限认证.
``` python
headers = {
    'appid': '此处填入接口验证ID'
}
````

# 用例公共函数
```python
def get_file_name(file_path):
    """获取文件名"""
    return file_path.split(r'/')[-1]

def read_audio(audio_path):
    """读取音频"""
    with open(audio_path, 'rb') as f:
        audio_content = f.read()
    return audio_content

def register(audio_path, group='ceshi'):
    """声纹注册"""
    url = "http://192.168.0.1:8100/v1/vpr/register"
    headers = {
        'appid': '此处填入接口验证ID'
    }
    audio_name = get_file_name(audio_path)
    data = {'group': group}
    files = [('train', (audio_name, read_audio(audio_path)))]
    res = requests.post(url, data=data, files=files, headers=headers).json()
    return res
```
