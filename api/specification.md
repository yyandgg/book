# 接口规范

## 1.请求头域内容（HTTP Request Header）

---

API服务需要在请求的HTTP头域中包含以下信息：

* host（必填）
* content-type（必填）
* content-length（选填）
* apiPublicKey\(必填\) 
* apiNonce\(必填\)  
* apiExecTime\(必填\)  
* apiClientCode\(必填\) 
* apiCheckSum\(必填\) 

作为示例，以下是一个标准的用户查询指定模板时的请求头域内容:

```
GET /api/v{version}/profile/{profile_name} HTTP/1.1
accept-encoding: gzip, deflate
host: media.pontus.com
accept: */*
content-type: application/json
connection: keep-alive
apiPublicKey: client1xxxxxx
apiNonce: 938219048
apiClientCode: client1
apiExecTime：17893213213213213
apiCheckSum：431439240324324
```

## 2.请求消息体格式（HTTP Request Body）

---

音视频转码的API服务要求使用JSON格式的结构体来描述一个请求的具体内容。

作为示例，以下是一个标准的用户创建新频道时的请求消息体格式：

```
{
  "cid": "pontus_0001",
  "screen_mode": "2-RIGHT",
  "profile_name": "video_mp4_1280x720_1728kbps",
  "type": 1,
  "show_id": false
}
```

## 3.请求返回格式（HTTP Response）

---

音视频转码的API服务均采用JSON格式的消息体作为响应返回的格式。

作为示例，以下是一个标准的用户查询频道时的完整请求返回：


```
HTTP/1.1 200 OK
Transfer-Encoding: chunked
Cache-Control: no-cache
Server: PWS
Date: Tue, 24 Mar 2015 13:34:07 GMT
Content-Type: application/json;charset=UTF-8

{
  "channels" : [
  {
    "cid": "pontus_0001",
    "screen_mode": "2-RIGHT",
    "profile_name": "video_mp4_1280x720_1728kbps",
    "type": 1,
    "show_id": false,
    "max_member": 8,
    "create_time": "2015-05-19T11:40:39Z"
  }
  ]
}
```

## 4.API Key 鉴权

API Key 用于标识用户及接口鉴权。所有用户的GET/POST/PUT/DELETE接口消息，均需要设置在HTTP请求头中。

| 参数 | 类型 | 必填域 | 说明 |
| --- | --- | --- | --- |
| apiPublicKey | String | 是 | 平台分配的公匙 |
| apiNonce | String | 是 | 随机数字字符串（最长64个字符） |
| apiClientCode | String | 是 | 用户标示字符串 |
| apiExecTime | String | 是 | UTC时间戳，转为秒数 |
| apiCheckSum | String | 是 | 平台验证消息合法性验证码；验证方法是 SHA1\(平台私匙 + apiNonce + apiClientCode + apiExecTime\) |

## 5.错误信息格式


| **错误码** | **错误信息** | **描述** | **HTTP状态码** |
| --- | --- | --- | --- |
| NoSuchProfile | The requested profile does not exist. Please double confirm your preserId or the existence of the profile. | 所访问的Profile不存在，请重新确定指定的profileName是否正确或确认指定Profile是否存在。 | 404 |
| NoSuchTask | The requested task does not exist. Please confirm your task_id or the existence of the task. | 所访问的Task不存在，请重新确定指定的task_id是否正确或确认指定Task是否存在。 | 404 |
| ProfileNotEmpty | Profile has tasks applied in pending or running status. Please wait for the tasks to be completed and try again. | 使用该模板任务尚有处在在等待或运行中的状态，请等待使用该模板的任务全部完成。 | 400 |
| InvalidParameterException | There are field\(s\) invalied in the request messsage body, please check. | 请求的结构体中包含一个或者多个字段错误，请检查确认。 | 400 |

