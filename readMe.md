readMe
# commande对外接口

### 头部公共参数
| 参数名称 | 参数类型 |是否必选 |参数描述|
| -----| ---- |-----| ---- |
| auth_token      | String | 是   | 用户授权 |

### 返回体格式

| 参数名称          | 参数类型       |  参数说明         |
| ----------------- | ---------- | --------------------------- |
| code             | String         |  状态码               |
| data              | Object       |  返回参数           |
| message      | String        |  提示信息           |

data在一些操作类API的返回中可能为空。

例如：
```json
{
  "code": "000000",
  "data": ""
  "message": "S_SUCCESS"
}
```

```json
{
  "code": "000000",
  "data": {
	"id": "F8CE226C6A6B4294B0440C9A3848D5A7",
	"name": "科大讯飞股份有限公司"
	},
  "message": ""
}
```
	
```json
{
  "code": "900004",
  "data": "", 
  "message": "未知的错误"
}
```

状态码：

| 编码 | 说明 |
| -----| ---- |
| 000000   |   成功   |
| 900001    |   无token，请登录   |
| 900002    |   token失效，请登录   |
| 900004    |   未知错误   |




#### 1.列表 
**接口描述** :  RPA控制中心机器人列表

**访问地址** :  http://172.31.94.23:10241

**请求路径** :  /commander/robot/external/my-robot-list

**请求方式** :  GET

```json
curl: http://172.31.94.23:10243/commander/robot/external/my-robot-list
```
**请求参数**:

|    参数名称    |  参数类型   |  最大长度  |  是否必填   |   参数说明  |
| ----------------- | -------------   | -------------   | -------------   | -------------  |
|  pageNo        |    Integer   |        --        |   否    |    页码     |
|  pageSize      |   Integer   |         --       |    否 |      分页大小   |
|  robotName   |   String      |       64        |   否  |  机器人名称   |
|  connStatus   |   String     |          1       |   否     |   连接状态：0-未连接,1-连接  |
|  scheduleStatus   |  String   |        1        |  否   |   调度状态：0-不可调度,1-可调度    |

**返回参数**:

| 参数名称       | 参数类型 | 参数说明 |
| -------------- | -------- | -------- |
| id             |    Integer      |    机器人主键ID      |
| profileId      |    Integer      |     机器人扩展信息表主键ID    |
| uuid           |      String    |      机器人本地 uuid 信息    |
| name           |     String     |     机器人名称     |
| creatorId      |      Integer    |      创建者ID    |
| groupId        |     Integer     |       Robot所属的组ID   |
| createTime     |     LocalDateTime     |     创建时间     |
| updateTime     |     LocalDateTime     |     启动时间     |
| isDeleted      |    Boolean      |    删除标志位      |
| robotId        |    Integer      |     机器人列表主键id     |
| nickName       |    String      |    机器人别名      |
| description    |   String       |      机器人描述    |
| version        |    String      |    版本信息      |
| nodeName       |     String     |      节点信息    |
| nodeIp         |       String   |     节点IP信息     |
| macAddress     |   String       |    节点的 MAC 地址      |
| nodeRobotDirs  |     String     |     机器人目录信息     |
| result         |      Integer    |      执行结果： 0-成功,1-失败,2-取消    |
| connStatus     |     Integer     |     连接状态：0-未连接,1-连接     |
| scheduleStatus |    Integer      |    调度状态:0-不可调度,1-可调度      |
| icon           |    String      |     机器人在本地的Icon信息     |
| progress       |     Double     |    执行进度      |
| lastExecTime          |     LocalDateTime     |      机器人上次启动时间    |

**分页参数**:
|参数名称|参数类型|参数说明|
| ----------- | ------- | --- |
| current     | Integer |  当前页   |
| hitCount    | boolean |   --  |
| searchCount | boolean |  --   |
| size        | Integer |  分页大小   |
| pages       | Integer |  分页总数   |
| records     | Object集合  |   返回值对象集合  |
| total       | Integer |  总条数  |

**返回示例**:
```json
{
    "code": "000000",
    "data": {
        "records": [
            {
                "id": null,
                "profileId": 5679,
                "uuid": "Rgzismh5fkf40",
                "name": "aaa1",
                "creatorId": 201,
                "groupId": 1,
                "createTime": "2021-12-03 16:48:26",
                "updateTime": "0001-01-01 00:00:00",
                "isDeleted": false,
                "robotId": 45627,
                "nickName": null,
                "description": "",
                "version": null,
                "nodeName": null,
                "nodeIp": "10.1.199.83",
                "macAddress": "58:6c:25:f4:bc:68",
                "nodeRobotDirs": "C:\\Users\\kqzhu\\Desktop",
                "result": null,
                "connStatus": 0,
                "scheduleStatus": 1,
                "icon": "robot_icon15",
                "progress": null,
                "lastExecTime": "0001-01-01 00:00:00"
            }
        ],
        "total": 1,
        "size": 20,
        "current": 1,
        "orders": [],
        "optimizeCountSql": true,
        "hitCount": false,
        "searchCount": true,
        "pages": 1
    },
    "message": ""
}
```

#### 2.启用机器人

**接口描述** :  RPA控制中心启动机器人

**访问地址** :  http://172.31.94.23:10241

**请求路径** :  /commander/robot/external/start-robot

**请求方式** :  POST

```json
 curl -H  "Content-Type:x-www.form-urlencoded" -X POST --data

 "prefileId":23434

 http://172.31.94.23:10243/commander/robot/external/start-robot
```
**请求参数**:

|    参数名称    |  参数类型   |  最大长度  |  是否必填   |   参数说明  |
| ----------------- | -------------   | -------------   | -------------   | -------------  |
|  prefileId       |    Integer   |     64       |   是   |    机器人扩展信息表主键ID   |

#### 3.停止

**接口描述** :  RPA控制中心停止机器人

**访问地址** :  http://172.31.94.23:10241

**请求路径** :  /commander/robot/external/stop-robot

**请求方式** :  POST

```json
 curl -H  "Content-Type:x-www.form-urlencoded" -X POST --data

 "prefileId":23434

 http://172.31.94.23:10243/commander/robot/external/stop-robot
```
**请求参数**:

|    参数名称    |  参数类型   |  最大长度  |  是否必填   |   参数说明  |
| ----------------- | -------------   | -------------   | -------------   | -------------  |
|  prefileId       |    Integer   |     64       |   是   |    机器人扩展信息表主键ID   |
