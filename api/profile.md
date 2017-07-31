# 模板接口（Profile API）

## 创建模板

---

**接口描述**

当系统预设的Profile无法满足需求时，用户可以通过此接口创建自定义的Profile。

**请求（Request）**

* 请求语法：

```
POST /api/v{version}/profile HTTP/1.1
accept-encoding: gzip, deflate
connection: keep-alive
accept: */*
host: media.pontus.com
content-type: application/json
apiPublicKey: {api-public-key}  
apiNonce: {api-nonce}
apiClientCode: {api-client-code}
apiExecTime：{api-exec-time} 
apiCheckSum：{api-check-sum}
```

* 请求头域：无特殊Header参数

* 请求参数：

| **字段名称** | **字段类型** | **必要性** | **字段描述** | **可选值** | **默认值** |
| --- | --- | --- | --- | --- | --- |
| profile\_name | String | 必选 | 模板模板名称 | - | - |
| description | String | 可选 | 转码模板描述 | - | - |
| qlties | Object | 必选 | 转码参数组（一个模板可以包括多组转码参数） | - | - |
| - container | String | 必选 | 音视频文件的容器 | "flv", "mp4", "m3u8", "mpegts", "copy" | - |
| - format | String | 可选 | 视频编码格式，copy表示透传（其他视频处理参数将被忽略） | "mpeg2", "h264", "h265" | "h264" |
| - bitrate | Number | 必选 | 视频输出码率 | 大于0 | - |
| - framerate | String | 可选 | 视频输出帧率 | "12/1", "15/1", "24000/1001", "24/1", "25/1", "30000/1001", "30/1", "60/1" | 不填写，表示与输入一致 |
| - width | Number | 可选 | 视频输出宽度 | 64 ~ 4096 | 不填写，表示与原始视频保持一致 |
| - height | Number | 可选 | 视频输出高度 | 64 ~ 4096 | 不填写，表示与原始视频保持一致 |
| - use\_progressive | String | 可选 | 选择使用逐行扫描（Progressive）/隔行扫描（Interlace） | "true", "false" | "true" |
| - gop\_size | Number | 可选 | GOP长度 | 12, 15, 20, 24, 25, 30, 48, 50, 60, 100, 120 | 50 |
| - b\_frame\_size | Number | 可选 | B帧数量 | 0, 1, 2, 3 | 0 |
| - rc\_mode | String | 可选 | 码率控制模式 | "cbr", "vbr", "2passvbr" | "cbr" |
| - preset | String | 可选 | 预设模式 | "default", "highQuality", "highPerformance" | "default" |
| - audio\_format | String | 可选 | 音频编码格式，copy表示透传（其他音频处理参数将被忽略） | "aac", "aache2", "mp3", "ac3", "mp2", "copy" | "aac" |
| - audio\_bitrate | Number | 必选 | 音频输出码率 | 大于0 | - |
| - audio\_samplerate | Number | 可选 | 音频采样率； | 8000, 11025, 16000, 22050, 24000, 32000, 44100, 48000, 64000, 88200, 96000 | 不填写，表示与输入保持一致 |
| - channels | Number | 可选 | 音频声道数目 | 1, 2, 6 | 不填写，表示与输入一致 |

* 请求示例：

```
POST /api/v0/profile HTTP/1.1
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
  "profile_name": "customlized_profile",
  "description": "A example preset description",
  "qlties":
  [
    {
      "container": "mp4",
      "format": "h264",
      "bitrate": 8000000,
      "framerate": 30,
      "width": 4096,
      "height": 2160,
      "audio_bitrate": 256000
    }
  ]
}
```

**响应（Response）**

* 响应头域：无特殊Header参数

* 响应参数：无

* 响应示例：

```
HTTP/1.1 200 OK
Transfer-Encoding: chunked
Cache-Control: no-cache
Server: PWS
Date: Tue, 24 Mar 2015 13:37:10 GMT
Content-Type: application/json;charset=UTF-8
```

## 查询指定模板

---

**接口描述**

通过profile_name查询指定的模板信息。

**请求（Request）**

* 请求语法：

```
GET /api/v{version}/profile/{profile_name} HTTP/1.1
accept-encoding: gzip, deflate
connection: keep-alive
accept: */*
host: media.pontus.com
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
GET /api/v0/profile/video_mp4_1920x1080_3660kbps HTTP/1.1
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

* 响应参数：与\[\#3.4 创建模板/请求/请求参数\]保持一致，增加一下字段；

| **字段名称** | **字段类型** | **字段描述** |
| --- | --- | --- |
| created\_time | String | 模板创建的UTC格式的时间 |
| qlties\_length | Number | 模板包含的编码参数组数 |

* 响应示例：

```
HTTP/1.1 200 OK
Transfer-Encoding: chunked
Cache-Control: no-cache
Server: BWS
Date: Tue, 24 Mar 2015 13:37:10 GMT
Content-Type: application/json;charset=UTF-8

{ 
  "create_time": "2016-09-23T02:00:59.258702Z", 
  "profile_name": "customlized_profile", 
  "qlties_length": 1, 
  "qlties": [ 
    { 
      "container": "mp4",
      "format": "h264",
      "bitrate": "8000000",
      "framerate": "30",
      "width": "4096",
      "height": "2160",
      "use_progressive": "true",
      "gop_size": "50",
      "b_frame_num": "0",
      "rc_mode": "cbr",
      "preset": "default",
      "audio_format": "aac",
      "audio_bitrate": "256000",
      "audio_samplerate": "0",
      "audio_channels": "0", 
      "template": "4", 
      "bitrate_is_customed": "true", 
      "live_streaming": "false",
      "hls_list_size": "10",
      "hls_time": "8"
    } 
  ] 
}
```

## 查询当前用户模板及所有系统模板

---

**接口描述**

用户查询其名下及系统提供的所有的模板，具体有哪些系统模板可以参考系统内置模板。

**请求（Request）**

* 请求语法：

```
GET /api/v{version}/profiles HTTP/1.1
accept-encoding: gzip, deflate
connection: keep-alive
accept: */*
host: media.pontus.com
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
GET /api/v0/profiles HTTP/1.1
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

* 响应参数：与\[创建模板\]保持一致，增加以下字段；

| **字段名称** | **字段类型** | **字段描述** |
| --- | --- | --- |
| created\_time | String | 模板创建的UTC格式的时间 |
| qlties\_length | Number | 模板包含的编码参数组数 |

* 响应示例：

```
HTTP/1.1 200 OK
Transfer-Encoding: chunked
Cache-Control: no-cache
Server: PWS
Date: Tue, 24 Mar 2015 13:37:10 GMT
Content-Type: application/json;charset=UTF-8

{
  "profiles": [
  {
    "create_time": "2016-09-23T02:00:59.258702Z",
    "profile_name": "customlized_profile",
    "qlties_length": 1,
    "qlties": [
    {
      "container": "mp4",
      "format": "h264",
      "bitrate": "8000000",
      "framerate": "30",
      "width": "4096",
      "height": "2160",
      "use_progressive": "true",
      "gop_size": "50",
      "b_frame_num": "0",
      "rc_mode": "cbr",
      "preset": "default",
      "audio_format": "aac",
      "audio_bitrate": "256000",
      "audio_samplerate": "0",
      "audio_channels": "0",
      "template": "4",
      "bitrate_is_customed": "true",
      "live_streaming": "false",
      "hls_list_size": "10",
      "hls_time": "8"
    }
    ]
  }
  ]
}
```

## 删除指定模板

---

**接口描述**

用于删除用户指定profile_name的用户模板

**请求（Request）**

* 请求语法：

```
DELETE /api/v{version}/profile/{profile_name} HTTP/1.1
accept-encoding: gzip, deflate
connection: keep-alive
accept: */*
host: media.pontus.com
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
DELETE /api/v0/profile/user-video-mp4-1080p-3660kbps HTTP/1.1
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
* 响应参数：无

* 响应示例：

```
HTTP/1.1 200 OK
Cache-Control: no-cache
```