# 互动直播接口（ILVB API）

## 加入互动直播

---

**接口描述**

创建互动直播频道后，使用该接口加入互动直播。

**请求（Request）**

* 请求语法：

```
  POST /api/v{version}/channel/ilvb HTTP/1.1
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
| input\_url | String | 必填 | 请求加入互动直播的输入URL |
| display\_type | String | - | 显示类型（特效类型），默认为普通模式 |
| id\_name | String | - | 标识名称（可以通过频道设置显示在互动窗口上），默认为空 |

* 请求示例：

```
  POST /api/v1/channel/ilvb HTTP/1.1
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
    "input_url": "rtmp://192.168.1.201/live/ilvb_member_1",
    "display_type": "normal",
    "id_name": "测试用户1"
  }
```

**响应（Response）**

* 响应头域：无特殊Header参数

* 响应参数：


| **字段名称** | **字段类型** | **字段描述** |
| --- | --- | --- |
| cid | String | 频道ID |
| member\_id | Number | 互动直播成员ID |
| output\_url | String | 互动直播输出媒体流URL |

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
    "member_id": 1,
    "output_url": "rtmp://192.168.1.204/ilvb/output1"
  }
```

## 退出互动直播

---

**接口描述**

退出互动直播。

**请求（Request）**

* 请求语法：

```
  DELETE /api/v{version}/channel/ilvb/{member_id} HTTP/1.1
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
  DELETE /api/v1/channel/ilvb/1 HTTP/1.1
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

## 获取指定互动直播成员信息

---

**接口描述**

通过频道ID（cid）查询指定的互动直播成员信息。

**请求（Request）**

* 请求语法：

```
  GET /api/v{version}/channel/{cid}/members HTTP/1.1
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
  GET /api/v1/channel/pontus_0001/members HTTP/1.1
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
| cid | String | 频道ID |
| member\_id | Number | 互动直播成员ID |
| input\_url | String | 输入URL |
| display\_type | String | 显示类型（特效类型） |
| id\_name | String | 标识名称（可以通过频道设置显示在互动窗口上） |

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
    "members" : [
    {
      "member_id": 1,
      "input_url": "rtmp://192.168.1.201/live/ilvb_member_1",
      "display_type": "normal",
      "id_name": "测试用户1"
    },
    {
      "member_id": 2,
      "input_url": "rtmp://192.168.1.201/live/ilvb_member_2",
      "display_type": "normal",
      "id_name": "测试用户2"
    }
    ]
  }
```
