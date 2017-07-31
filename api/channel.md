# 频道接口（Channel API）

## 创建直播频道

---

**接口描述**

用户通过该接口创建直播频道。

**请求（Request）**

* 请求语法：

```
POST /api/v{version}/channel HTTP/1.1
accept-encoding: gzip, deflate
connection: keep-alive
accept: */* host: media.pontus.com
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
| cid | String | 必填 | 频道ID，具有唯一性 |
| screen_mode | String | - | 分屏模式，默认是一个窗口 |
| profile_name | String | 必填 | 编码模板 |
| type | Number | 必填 | 频道类型：0为直播， 1为互动直播 |
| show_id_name | Boolean | - | 是否显示互动窗口标识名称（比如昵称），默认为false |

* 请求示例：

```
POST /api/v1/channel HTTP/1.1
accept-encoding: gzip, deflate
connection: keep-alive
accept: */* host: media.pontus.com
content-type: application/json
apiPublicKey: client1xxxxxx
apiNonce: 938219048
apiClientCode: client1
apiExecTime：17893213213213213
apiCheckSum：431439240324324

{
  "cid": "pontus_0001",
  "screen_mode": "2-RIGHT",
  "profile_name": "video_mp4_1280x720_1728kbps",
  "type": 1,
  "show_id_name": false
}
```

**响应（Response）**

* 响应头域：无特殊Header参数* 响应参数：

| **字段名称** | **字段类型** | **字段描述** |
| --- | --- | --- |
| cid | String | 频道ID |
| max_member | Number | 最大成员数 |
| create_time | String | 频道建立时间 |

* 响应示例：

```
HTTP/1.1 200 OK
Transfer-Encoding: chunked
Cache-Control: no-cache
Server: PWS
Date: Tue, 24 Mar 2015 13:34:07 GMT
Content-Type: application/json;charset=UTF-8

{
  "cid": "pontus_0001",
  "max_member": 8,
  "create_time": "2015-05-19T11:40:39Z"
}
```

## 获取频道列表

---

**接口描述**

查询所有频道。

**请求（Request）**

* 请求语法：

```
GET /api/v{version}/channels HTTP/1.1
accept-encoding: gzip, deflate
connection: keep-alive
accept: */* host: media.pontus.com
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
GET /api/v1/channels HTTP/1.1
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
| cid | String | 频道的唯一标示 |
| screen_mode | String | 分屏模式 |
| profile_name | String | 编码模板 |
| type | Number | 频道类型：0为直播， 1为互动直播 |
| show_id | Boolean | 是否显示互动窗口标识（比如昵称） |
| max_member | Number | 最大成员数 |
| create_time | String | 频道建立时间 |

* 响应示例：

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

## 获取指定频道

---

**接口描述**

查询指定频道ID（cid）的频道。

**请求（Request）**

* 请求语法：

```
GET /api/v{version}/channel/{cid} HTTP/1.1
accept-encoding: gzip, deflate
connection: keep-alive
accept: */* host: media.pontus.com
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
GET /api/v1/channel/pontus_0001 HTTP/1.1
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
| cid | String | 频道的唯一标示 |
| screen_mode | String | 分屏模式 |
| profile_name | String | 编码模板 |
| type | Number | 频道类型：0为直播， 1为互动直播 |
| show_id | Boolean | 是否显示互动窗口标识（比如昵称） |
| max_member | Number | 最大成员数 |
| create_time | String | 频道建立时间 |

* 响应示例：

```
HTTP/1.1 200 OK
Transfer-Encoding: chunked
Cache-Control: no-cache
Server: PWS
Date: Tue, 24 Mar 2015 13:34:07 GMT
Content-Type: application/json;charset=UTF-8

{
  "cid": "pontus_0001",
  "screen_mode": "2-RIGHT",
  "profile_name": "video_mp4_1280x720_1728kbps",
  "type": 1,
  "show_id": false,
  "max_member": 8,
  "create_time": "2015-05-19T11:40:39Z"
}
```

## 删除指定频道

---

**接口描述**

删除指定频道ID（cid）的频道。

**请求（Request）**

* 请求语法：

```
DELETE /api/v{version}/channel/{cid} HTTP/1.1
accept-encoding: gzip, deflate
connection: keep-alive
accept: */* host: media.pontus.com
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
DELETE /api/v1/channel/pontus_0001 HTTP/1.1
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

## 更新指定频道

---

**接口描述**

设置指定频道ID（cid）的频道信息。

**请求（Request）**

* 请求语法：

```
PUT /api/v{version}/channel/{cid} HTTP/1.1
accept-encoding: gzip, deflate
connection: keep-alive
accept: */* host: media.pontus.com
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
| screen_mode | String | - | 分屏模式 |
| profile_name | String | - | 编码模板 |
| type | Number | - | 频道类型：0为直播， 1为互动直播 |
| show_id_name | Boolean | - | 是否显示互动窗口标识名称（比如昵称） |

* 请求示例：

```
PUT /api/v1/channel/pontus_0001 HTTP/1.1
accept-encoding: gzip, deflate
connection: keep-alive
accept: */* host: media.pontus.com
content-type: application/json
apiPublicKey: client1xxxxxx
apiNonce: 938219048
apiClientCode: client1
apiExecTime：17893213213213213
apiCheckSum：431439240324324

{
  "screen_mode": "2-LEFT",
  "show_id_name": true
}
```

**响应（Response）**

* 响应头域：无特殊Header参数

* 响应参数：无

* 响应示例：

```
HTTP/1.1 200 OK
Cache-Control: no-cache
```