# 媒体信息接口（MediaInfo API）

## 查询指定媒体信息

---

**接口描述**

用户通过文件存储地址URL获取指定音视频文件的媒体信息。

**请求（Request）**

* 请求语法：

  ```
  GET /api/v{version}/mediainfo?url=samplepath%2Fsample.mp4 HTTP/1.1
  accept-encoding: gzip, deflate
  x-bce-date: {utc-date-string}
  host: media.bj.baidubce.com
  accept: */*
  connection: keep-alive
  x-bce-request-id: {bce-request-id}
  content-type: application/json
  authorization: {bce-authorization-string}
  ```

* 请求头域：无特殊Header参数

* 请求参数：无

* 请求示例：

  ```
  GET /api/v1/mediainfo?url=sampleforderpath%2Fsampleoutput.mp4 HTTP/1.1
  accept-encoding: gzip, deflate
  x-bce-date: 2015-03-24T13:37:10Z
  host: media.bj.baidubce.com
  accept: */*
  connection: keep-alive
  x-bce-request-id: 3807ce30-5264-45f2-9b52-26b78e24a750
  content-type: application/json
  authorization: bce-auth-v1/46bd9968a6194b4bbdf0341f2286ccce/2015-03-24T13:37:10Z/1800/host;x-bce-date/3e1bf9f50ae1fca2d704d61567810dde946fff3ca2e455676455a6f5c8cce596
  ```


**响应（Reponse）**

* 响应头域：无特殊Header参数
* 响应参数：

| **字段名称** | **字段类型** | **字段描述** |
| --- | --- | --- |
| url | String | 音视频文件所在的存储位置 |
| fileSizeInByte | Number | 音视频文件的大小 |
| durationInSecond | Number | 音视频媒体时长 |
| container | String | 音视频文件的容器类型 |
| type | String | 文件类型 |
| video | Object | 视频信息集合 |
| + codec | String | 视频文件的编码规格 |
| + heightInPixel | Number | 视频高度 |
| + widthInPixel | Number | 视频宽度 |
| + bitRateInBps | Number | 视频媒体的码流 |
| + frameRate | Number | 视频媒体的帧率 |
| audio | Object | 音频信息集合 |
| + codec | String | 音频文件的编码规格 |
| + channels | Number | 音频文件的声道信息 |
| + sampleRateInHz | Number | 音频文件的采样率 |
| + bitRateInBps | Number | 音频文件的码率 |

* 响应示例：

  ```
  HTTP/1.1 200 OK
  Transfer-Encoding: chunked
  x-bce-request-id: 3807ce30-5264-45f2-9b52-26b78e24a750
  Cache-Control: no-cache
  Server: BWS
  Date: Tue, 24 Mar 2015 13:37:10 GMT
  Content-Type: application/json;charset=UTF-8

  {
      "url": "samplefolderpath/sampleoutput.mp4",
      "fileSize": 102400,
      "durationInSecond": 60,
      "container": "mp4",
      "type": "video",
      "video": {
          "codec": "h264",
          "heightInPixel": 1024,
          "widthInPixel": 768,
          "bitRateInBps": 2500
      },
      "audio": {
          "codec": "acc",
          "channels": 2,
          "sampleRateInHz": 96000,
          "bitRateInBps": 1100
      }
  }
  ```


