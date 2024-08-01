# 实例 API

## 实例列表

```http
GET /api/service/remote_service_instances
```

#### 查询参数

```js
{
  daemonId: string;
  page: number;
  page_size: number;
  instance_name?: string;
  status: string;
}
```

#### 响应

```json
{
  "status": 200,
  "data": {
    "maxPage": 1,
    "pageSize": 10,
    "data": InstanceDetail[]
  },
  "time": 1718594177859
}
```

## 实例详细信息

```http
GET /api/instance
```

#### 查询参数

```js
{
  uuid: string,     // Instance ID
  daemonId: string,
}
```

#### 响应

```json
{
  "status": 200,
  "data": InstanceDetail,
  "time": 1718594177859
}
```

## 创建

```http
POST /api/instance
```

##### 查询参数

```js
{
  daemonId: string;
}
```

##### 请求参数

> [InstanceDetail](#type-of-instancedetail)

#### 响应

```json
{
  "status": 200,
  "data": {
    "instanceUuid": "50c73059001b436fa85c0d8221c157cf",
    "config": InstanceConfig
  },
  "time": 1718594177859
}
```

## 更新设置

```http
PUT /api/instance
```

#### 查询参数

```js
{
  uuid: string,     // Instance ID
  daemonId: string,
}
```

#### 请求参数

> [InstanceConfig](#type-of-instanceconfig)

#### 响应

```json
{
  "status": 200,
  "data": {
    "instanceUuid": "50c73059001b436fa85c0d8221c157cf"
  },
  "time": 1718594177859
}
```

## 删除

```http
DELETE /api/instance
```

#### 查询参数

```js
{
  daemonId: string,
}
```

#### 请求参数

```json
{
  "uuids": [
    "50c73059001b436fa85c0d8221c157cf"
    "11c2f4c89b9e4e1da819dc56bf16f151"
  ], // Instance Id
  "deleteFile": false // Delete instance files
}
```

#### 响应

```json
{
  "status": 200,
  "data": true,
  "time": 1718594177859
}
```

## 启动

```http
GET /api/protected_instance/open
```

#### 查询参数

```js
{
  uuid: string,     // Instance ID
  daemonId: string,
}
```

#### 响应

```json
{
  "status": 200,
  "data": {
    "instanceUuid": "50c73059001b436fa85c0d8221c157cf"
  },
  "time": 1718594177859
}
```

## 停止

```http
GET /api/protected_instance/stop
```

#### 查询参数

```js
{
  uuid: string,     // Instance ID
  daemonId: string,
}
```

#### 响应

```json
{
  "status": 200,
  "data": {
    "instanceUuid": "50c73059001b436fa85c0d8221c157cf"
  },
  "time": 1718594177859
}
```

## 重启

```http
GET /api/protected_instance/restart
```

#### 查询参数

```js
{
  uuid: string,     // Instance ID
  daemonId: string,
}
```

#### 响应

```json
{
  "status": 200,
  "data": {
    "instanceUuid": "50c73059001b436fa85c0d8221c157cf"
  },
  "time": 1718594177859
}
```

## Kill

```http
GET /api/protected_instance/kill
```

#### 查询参数

```js
{
  uuid: string,     // Instance ID
  daemonId: string,
}
```

#### 响应

```json
{
  "status": 200,
  "data": {
    "instanceUuid": "50c73059001b436fa85c0d8221c157cf"
  },
  "time": 1718594177859
}
```

## 批量操作
Support operations: `start`, `stop`, `restart`, `kill`

```http
POST /api/instance/multi_{{operations}}
```

#### 查询参数

```js
{
  instanceUuid: string,
  daemonId: string,
}[]
```

#### 响应

```json
{
  "status": 200,
  "data": true,
  "time": 1718594177859
}
```


## 更新实例

```http
GET /api/protected_instance/asynchronous
```

#### 查询参数

```js
{
  uuid: string,     // Instance ID
  daemonId: string,
  task_name: "update"
}
```

#### 响应

```json
{
  "status": 200,
  "data": true,
  "time": 1718594177859
}
```

## Send Command

```http
GET /api/protected_instance/command
```

#### 查询参数

```js
{
  uuid: string,     // Instance ID
  daemonId: string,
  command: string
}
```

#### 响应

```json
{
  "status": 200,
  "data": {
    "instanceUuid": "50c73059001b436fa85c0d8221c157cf"
  },
  "time": 1718594177859
}
```

## Get output

```http
GET /api/protected_instance/outputlog
```

#### 查询参数

```js
{
  uuid: string,     // Instance ID
  daemonId: string,
  size?: number      // Log size: 1KB ~ 2048KB
                     // if not set, return all logs
}
```

#### 响应

```json
{
  "status": 200,
  "data": "[INFO]: Done (12.138s)! For help, type \"help\"\n",
  "time": 1718594177859
}
```

## Reinstall

```http
POST /api/protected_instance/install_instance
```

#### 查询参数

```js
{
  daemonId: string,
  uuid: string      // Instance ID
}
```

#### 请求参数

```json
{
  "targetUrl": "https://files.example.com/Paper-1.20.4.zip",
  "title": "Minecraft 1.20.4 Java",
  "description": "[Paper] Low hardware configuration machine use, Fast setup."
}
```

#### 响应

```json
{
  "status": 200,
  "data": true,
  "time": 1718594177859
}
```

## Type of InstanceConfig

```json
{
  "nickname": "New Name",
  "startCommand": "cmd.exe",
  "stopCommand":  "^C",
  "cwd": "/workspaces/my_server/",
  "ie": "gbk",                        // input encode
  "oe": "gbk",                        // output encode
  "createDatetime": "2022/2/3",
  "lastDatetime": "2022/2/3 16:02",
  "type": "universal",                // instance type
  "tag": [],
  "endTime": "2022/2/28",
  "fileCode": "gbk",
  "processType": "docker",
  "updateCommand": "shutdown -s",
  "actionCommandList": [],
  "crlf": 2,
  "docker": DockerConfig,

  // Steam RCON
  "enableRcon": true,
  "rconPassword": "123456",
  "rconPort": 2557,
  "rconIp": "192.168.1.233",

  // Old fields
  "terminalOption": {
    "haveColor": false,
    "pty": true,
  },
  "eventTask": {
    "autoStart": false,
    "autoRestart": true,
    "ignore": false,
  },
  "pingConfig": {
    "ip": "",
    "port": 25565,
    "type": 1,
  }
}
```

## Type of InstanceDetail

```json
{
  "config": InstanceConfig,
  "info": {
    "currentPlayers": -1,
    "fileLock": 0,
    "maxPlayers": -1,
    "openFrpStatus": false,
    "playersChart": [],
    "version": "",
  },
  "instanceUuid": "50c73059001b436fa85c0d8221c157cf",
  "processInfo": {
    "cpu": 0,
    "memory": 0,
    "ppid": 0,
    "pid": 0,
    "ctime": 0,
    "elapsed": 0,
    "timestamp": 0
  },
  "space": 0,
  "started": 6, // start count
  "status": 3,  // -1 = busy,
                // 0  = stopped,
                // 1  = stopping,
                // 2  = starting,
                // 3  = running
}
```

## Type of Instance DockerConfig

```json
{
  "containerName": "",
  "image": "mcsm-ubuntu:22.04",
  "memory": 1024, // MB
  "ports": ["25565:25565/tcp"],
  "extraVolumes": [],
  "maxSpace": null,
  "network": null,
  "io": null,
  "networkMode": "bridge",
  "networkAliases": [],
  "cpusetCpus": "",
  "cpuUsage": 100,
  "workingDir": "",
  "env": []
}
```
