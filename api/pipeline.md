# 频道接口（Channel API） -- TODO

## 1. 频道创建

---

**接口描述**

上层管理接口，用户向云平台请求创建频道；返回频道的接收地址及发布地址；

**请求（Request）**

* 请求语法：

  ```
  POST /apiV{version}/pontus/channel/create HTTP/1.1
  accept-encoding: gzip, deflate
  connection: keep-alive
  accept: */*
  host: media.pontus.com
  apiPublicKey: client1xxxxxx  
  apiNonce: 938219048  
  apiClientCode: client1  
  apiExecTime：17893213213213213  
  apiCheckSum：431439240324324
  ```

  * 请求头域：无特殊Header参数
  * 请求参数：


| **参数名** | **参数类型** | **必要性** | **参数描述** |
| --- | --- | --- | --- |
| channelType | Int | 必填 | 频道类型（0：标准频道；1：互动频道） |
| streamType | Int | 必填 | 本频道流媒体类型（0：rtmp） |
| targetBucket | String | 必选 | 输出Bucket |
| config | Object | 必选 | 队列的配置 |
| + capacity | Number | 必选 | 队列的并发能力 |
| + notification | String | 可选 | 通知名称 |

* 请求示例：

  ```
  POST /v3/pipeline HTTP/1.1
  accept-encoding: gzip, deflate
  x-bce-date: 2015-03-24T13:02:00Z
  connection: keep-alive
  accept: */*
  host: media.pontus.com
  x-bce-request-id: 73c4e74c-3101-4a00-bf44-fe246959c05e
  content-type: application/json
  authorization: bce-auth-v1/46bd9968a6194b4bbdf0341f2286ccce/2015-03-24T13:02:00Z/1800/host;x-bce-date/994014d96b0eb26578e039fa053a4f9003425da4bfedf33f4790882fb4c54903

  {
      "sourceBucket": "exampleIuputBucket",
      "targetBucket": "exampletargetBucket",
      "pipelineName": "medium_priority_pipe",
      "description": "The pipeline holding medium priority jobs.",
      "config": {
          "capacity": "5",
          s"notification" : "mct_notification"
      }
  }
  ```

  **响应（Response）**

* 响应头域：无特殊Header参数

* 响应参数：无

* 响应示例：

  ```
  HTTP/1.1 200 OK
  x-bce-request-id: 73c4e74c-3101-4a00-bf44-fe246959c05e
  Cache-Control: no-cache
  Server: BWS
  Date: Tue, 24 Mar 2015 13:02:01 GMT
  Content-Type: application/json;charset=UTF-8
  ```


## 查询指定队列

---

**接口描述**

基本接口，用户通过指定name来查询该指定队列的信息。

**请求（Request）**

* 请求语法：

  ```
  GET /v{version}/pipeline/{pipelineName} HTTP/1.1
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
  GET /v3/pipeline/high_priority_pipe HTTP/1.1
  accept-encoding: gzip, deflate
  x-bce-date: 2015-03-24T13:04:26Z
  host: media.bj.baidubce.com
  accept: */*
  connection: keep-alive
  x-bce-request-id: 4cd11be3-fcaf-4ce5-aa4a-135f3c27b12b
  content-type: application/json
  authorization: bce-auth-v1/02296dd93f1940a39913d9a406332486/2015-03-24T13:04:26Z/1800/host;x-bce-date/0ffab05c5001f9d80c8d2630561ff2144cf070d1fe838133412c8245615046f9
  ```

  **响应（Response）**

* 响应头域：无特殊Header参数

* 响应参数


| **参数名** | **参数类型** | **参数描述** |
| --- | --- | --- |
| pipelineName | String | 用户指定的队列名称，允许小写字母、数字以及下划线且必须以字母开头 |
| sourceBucket | String | 用户指定的输入Bucket |
| targetBucket | String | 用户指定的输出Bucket |
| config | Object | 队列配置的对象 |
| + capacity | Number | 队列的并发能力 |
| + notification | String | 通知名称 |
| state | String | 队列状态，分为ACTIVE\/INACTIVE |
| createTime | String | 创建时间，UTC格式 |
| description | String | 用户指定的队列描述 |
| jobStatus | Object | 队列中任务的状态集合 |
| + total | Number | 队列中的任务总数 |
| + running | Number | 队列中运行中的任务总数 |
| + pending | Number | 队列中排队中的任务总数 |
| + success | Number | 队列中已执行成功的任务总数 |
| + failed | Number | 队列中执行失败的任务总数 |

* 响应示例：

  ```
  HTTP/1.1 200 OK
  Transfer-Encoding: chunked
  x-bce-request-id: 47281222-f0ff-4f80-9a4d-0140ff77dcd0
  Cache-Control: no-cache
  Server: BWS
  Date: Tue, 24 Mar 2015 13:04:27 GMT
  Content-Type: application/json;charset=UTF-8

  {
      "name": "high_priority_pipe",
      "sourceBucket": "exampleSourceBucket",
      "targetBucket": "exampleTargetBucket",
      "config": {
        "capacity": 5,
        "notification": "mct_notification"
      },
      "state":"ACTIVE",
      "createTime":"2015-03-24T13:04:26Z",
      "description":"A pipleine hoding high priority jobs.",
      "jobStatus":
      {
          "total": 10,
          "running": 2,
          "pending": 1,
          "success": 7,
          "failed": 1
      }
  }
  ```


## 查询用户所有队列

---

**接口描述**

易用性接口，帮助用户查询所拥有的所有队列的详细信息。

**请求（Request）**

* 请求语法：

  ```
  GET /v{version}/pipeline HTTP/1.1
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
  GET /v3/pipeline HTTP/1.1
  accept-encoding: gzip, deflate
  x-bce-date: 2015-03-24T13:03:20Z
  host: media.bj.baidubce.com
  accept: */*
  connection: keep-alive
  x-bce-request-id: cc7500cb-ebc5-4ac2-9018-4befad8e2479
  content-type: application/json
  authorization: bce-auth-v1/46bd9968a6194b4bbdf0341f2286ccce/2015-03-24T13:03:20Z/1800/host;x-bce-date/c5e36c982e5037841925c6729f1e74df53ebb134745d3e6da2722f2333d390a2
  ```


**响应（Response）**

* 响应头域：无特殊Header参数

* 响应参数：


| **参数名** | **参数类型** | **参数描述** |
| --- | --- | --- |
| pipelines | Object | 用户队列的集合 |
| + pipelineName | String | 用户指定的队列名称 |
| + sourceBucket | String | 用户指定的输入Bucket |
| + targetBucket | String | 用户指定的输出Bucket |
| + config | Object | 队列配置 |
| ++ capacity | Number | 队列的并发能力 |
| ++ notification | String | 通知名称 |
| + state | String | 队列状态，分为ACTIVE\/INACTIVE |
| + createTime | String | 创建时间，UTC格式 |
| + description | String | 用户指定的队列描述 |
| + status | Object | 队列中任务的状态集合 |
| ++ total | Number | 队列中的任务总数 |
| ++ running | Number | 队列中运行中的任务总数 |
| ++ pending | Number | 队列中排队中的任务总数 |
| ++ success | Number | 队列中已执行成功的任务总数 |
| ++ failed | Number | 队列中执行失败的任务总数 |

* 响应示例：

  ```
  HTTP/1.1 200 OK
  Transfer-Encoding: chunked
  x-bce-request-id: cc7500cb-ebc5-4ac2-9018-4befad8e2479
  Cache-Control: no-cache
  Server: BWS
  Date: Tue, 24 Mar 2015 13:03:21 GMT
  Content-Type: application/json;charset=UTF-8

  {
      "pipelines": [
          {
              "pipelineName": "high_priority_pipe",
              "sourceBucket": "sampleSourceBucket00",
              "targetBucket": "sampleTargetBucket00",
              "config": {
                  "capacity":20,
                  "notification": "mct_notification"
              },
              "state": "ACTIVE",
              "createTime": "2015-03-24T13:03:20Z",
              "description": "The pipeline holding high priority jobs.",
              "jobStatus": {
                  "total": 0,
                  "running": 0,
                  "pending": 0,
                  "success": 0,
                  "failed": 0
              }
          },
          {
              "pipelineName": "medium_priority_pipe",
              "sourceBucket": "sampleSourceBucket01",
              "targetBucket": "sampleTargetBucket01",
              "config": {
                  "capacity":20
              },
              "state": "ACTIVE",
              "createTime": "2015-03-24T13:03:20Z",
              "description": "The pipeline holding medium priority jobs.",
              "jobStatus": {
                  "total": 0,
                  "running": 0,
                  "pending": 0,
                  "success": 0,
                  "failed": 0
              }
          },
          {
              "pipelineName": "low_priority_pipe",
              "sourceBucket": "sampleSourceBucket02",
              "targetBucket": "sampleTargetBucket02",
              "config": {
                  "capacity":20
              },
              "state": "ACTIVE",
              "createTime": "2015-03-24T13:03:20Z",
              "description": "The pipeline holding low priority jobs.",
              "jobStatus": {
                  "total": 0,
                  "running": 0,
                  "pending": 0,
                  "success": 0,
                  "failed": 0
              }
          }
      ]
  }
  ```


## 删除指定队列

---

**接口描述**

基本接口，用户向服务请求删除指定pipelineName的任务队列。

**请求（Request）**

* 请求语法：

  ```
  DELETE /v{version}/pipeline/{pipelineName} HTTP/1.1
  accept-encoding: gzip, deflate
  x-bce-date: {utc-date-string}
  connection: keep-alive
  accept: */*
  host: media.bj.baidubce.com
  x-bce-request-id: {bce-request-id}
  content-type: application/json
  authorization: {bce-authorization-string}
  ```

* 请求头域：无特殊Header参数

* 请求参数：无

* 请求示例：

  ```
  DELETE /v3/pipeline/high_priority_pipe HTTP/1.1
  accept-encoding: gzip, deflate
  x-bce-date: 2015-03-24T13:06:02Z
  connection: keep-alive
  accept: */*
  host: media.bj.baidubce.com
  x-bce-request-id: 6d0b0a36-2ffe-49d4-9d81-333a9ab9417e
  content-type: application/json
  authorization: bce-auth-v1/46bd9968a6194b4bbdf0341f2286ccce/2015-03-24T13:06:02Z/1800/host;x-bce-date/02f64774999996903cffa5ae4d6eef436127a96f581a4e8467497e239d824be8
  ```


**响应（Response）**

* 响应头域：无特殊Header参数
* 响应参数：无

* 响应示例：

  ```
  HTTP/1.1 200 OK
  x-bce-request-id: 6d0b0a36-2ffe-49d4-9d81-333a9ab9417e
  Cache-Control: no-cache
  ```


