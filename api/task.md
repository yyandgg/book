# 视频转码任务接口（Task/Transcoding API）

## 创建视频转码任务

---

**接口描述**

用户通过该接口创建转码任务。

**请求（Request）**

* 请求语法：

```
POST /api/v{version}/task/transcoding HTTP/1.1
accept-encoding: gzip, deflate
connection: keep-alive
accept: */*
host: media.pontus.com
apiPublicKey: {api-public-key}  
apiNonce: {api-nonce}
apiClientCode: {api-client-code}
apiExecTime：{api-exec-time} 
apiCheckSum：{api-check-sum}
```

* 请求头域：无特殊Header参数

* 请求参数：

| **字段名称** | **字段类型** | **必要性** | **字段描述** |
| --- | --- | --- | --- |
| source | Object | 必填 | 输入的原始信息集合 |
| + source\_url | String | - | 源视频的URL，输入文件存储地址或实时流地址 |
| profile\_name | String | - | 输出处理的模板profile\_name |
| targets | Object | 必填 | 输出的信息组（一个转码任务可以包括多个输出） |
| - target\_url | String | - | 目标视频的URL，输出文件存储地址或实时流地址 |

* 请求示例：

```
POST /api/v1/task/transcoding HTTP/1.1
accept-encoding: gzip, deflate
connection: keep-alive
accept: */*
host: media.pontus.com
content-type: application/json
apiPublicKey: client1xxxxxx  
apiNonce: 938219048  
apiClientCode: client1  
apiExecTime：17893213213213213  
apiCheckSum：431439240324324

{
  "source": {
    "source_url": "rtmp://192.168.1.201/live/sample_1in2out"
  },
  "profile_name": "video_mp4_1280x720_1728kbps",
  "targets": [
  {
    "target_url": "rtmp://192.168.1.201/live/sample_out0"
  },
  {
    "target_url": "rtmp://192.168.1.201/live/sample_out1"
  }
  ]
}
```

**响应（Response）**

* 响应头域：无特殊Header参数

* 响应参数：

| **字段名称** | **字段类型** | **字段描述** |
| --- | --- | --- |
| task\_id | String | 系统生成的Task唯一标示task\_id |

* 响应示例：

```
HTTP/1.1 200 OK
Transfer-Encoding: chunked
Cache-Control: no-cache
Server: PWS
Date: Tue, 24 Mar 2015 13:34:07 GMT
Content-Type: application/json;charset=UTF-8

{
  "task_id":"3125"
}
```

## 查询指定视频转码任务

---

**接口描述**

通过指定task\_id查询该任务的信息。

**请求（Request）**

* 请求语法：

```
GET /api/v{version}/task/transcoding/{task_id} HTTP/1.1
accept-encoding: gzip, deflate
host: media.pontus.com
accept: */*
connection: keep-alive
content-type: application/json
apiPublicKey: {api-public-key}  
apiNonce: {api-nonce}
apiClientCode: {api-client-code}
apiExecTime：{api-exec-time} 
apiCheckSum：{api-check-sum}
```

* 请求头域：无特殊Header参数

* 请求参数：无

* 请求示例：

```
GET /api/v0/task/transcoding/3125 HTTP/1.1
accept-encoding: gzip, deflate
connection: keep-alive
accept: */*
host: media.pontus.com
content-type: application/json
apiPublicKey: client1xxxxxx  
apiNonce: 938219048  
apiClientCode: client1  
apiExecTime：17893213213213213  
apiCheckSum：431439240324324
```

**响应（Response）**

* 响应头域：无特殊Header参数

* 响应参数：

| **字段名称** | **字段类型** | **字段描述** |
| --- | --- | --- |
| task\_id | String | 任务的唯一标示 |
| source | Object | 输入的原始信息集合 |
| + source\_url | String | 源视频的URL，输入文件存储地址或实时流地址 |
| profile\_name | String | 输出处理的模板profile\_name |
| targets | Object | 输出的信息组（一个转码任务可以包括多个输出） |
| - target\_url | String | 目标视频的URL，输出文件存储地址或实时流地址 |
| task\_status | String | 任务状态 |
| error | Object | task失败时的错误信息，task\_status == TaskFail时存在 |
| +code | String | 错误码 |
| +message | String | 错误原因 |
| create\_time | String | 任务创建的时间 |
| start\_time | String | 任务开始处理的时间 |
| end\_time | String | 任务完成处理的时间 |

* 响应示例：

```
HTTP/1.1 200 OK
Transfer-Encoding: chunked
Cache-Control: no-cache
Server: PWS
Date: Tue, 24 Mar 2015 13:34:07 GMT
Content-Type: application/json;charset=UTF-8

{
  "task_id" : "3125",
  "source": {
    "source_url": "rtmp://192.168.1.201/live/sample_1in2out"
  },
  "profile_name": "video_mp4_1280x720_1728kbps",
  "targets": [
  {
    "target_url": "rtmp://192.168.1.201/live/sample_out0"
  },
  {
    "target_url": "rtmp://192.168.1.201/live/sample_out1"
  }
  ]
  "task_status" : "FAILED",
  "create_time" : "2015-05-19T12:28:39Z",
  "start_time" : "2015-05-19T12:28:41Z",
  "end_time" : "2015-05-19T12:28:44Z",
  "error" : {
    "code" : "ParameterError",
    "message" : "Parameter error"
  }
}
```

## 常见错误码和错误信息

---

转码任务常见的错误码及错误信息如下表所示：

| **错误码** | **错误信息** | **错误信息（控制台显示）** |
| --- | --- | --- |
| ParameterError | The input parameter is invalid. Please check it. | 输入参数错误，请检查输入参数 |
| InternalError | Internal error happened. | 内部错误 |
| InputNotSupported | The input format is not supported. | 输入的数据格式不支持 |
| OutputNotSupported | The output format is not supported. | 输出的数据格式不支持 |
| InvalidInputData | The input data is invalid. Please check your input data. | 无效的输入数据，请检查您的输入视频是否是有效 |
| TimeOut | Task time out. | 任务超时 |
| Unknown | Unknown error. | 未知错误 |