##创建任务

`POST /v1/jobs`

```json
{
  "name": "test",
  "namespace": "chennanfei",
  "command": "bash",
  "docker_image_repo": "index.alauda.cn/chennanfei/job_image",
  "docker_image_tag": "latest",
  "resource_size": "XXS",
  "is_schedule_active": false,
  "schedule_mode": null,
  "runtime_vars": {
    "DB_HOST": "localhost"
  }
}
```

**参数说明**

- **name**：任务名称，中英文均可

- **namespace**：任务所属的命名空间，即用户名或者组织名

- **command**：启动任务容器时执行的命令

- **docker_image_repo**：镜像仓库

- **docker_image_tag**：镜像版本

- **resource_size**：任务容器的实例大小，目前仅支持XXS、XS

- **region_name**：任务执行所在区，目前仅支持BEIJING1

- **is_schedule_active**：是否开启调度

- **schedule_mode**：调度模式，例如"R1/2015-12-31T16:00:23.446Z/PT1H"。R1表示重复1次；2015-11-12T16:00:23.446Z是任务开始时间（UTC）；PT1H表示每隔1小时执行一次。可参考[ISO 8601](http://baike.baidu.com/link?url=g12PRr654fZMQWbg2MQQ2KOJSlJp40dSvtYmUq-y-sPJx8fohJWi1QVZemdEWEX5USCm0NFj0kVkfpN3EHmlia)

- **runtime_vars**：任务容器运行时环境变量，例如

```json
{
  "ENDPOINT": "http://api.example.com",
  "USERNAME": "tester",
  "PASSWORD": "password"
}
```

**返回结果示例（status code：201）**

```json
{
  "id": 146,
  "created_by": "chennanfei",
  "command": "bash",
  "docker_image_repo": "index.alauda.cn/chennanfei/job_image",
  "docker_image_tag": "latest",
  "name": "test",
  "region_name": "BEIJING1",
  "namespace": "chennanfei",
  "created_at": "2015-12-28T14:31:07.639255+00:00",
  "updated_at": "2015-12-28T14:31:07.639296+00:00",
  "resource_size": "XXS",
  "schedule_mode": "R1/2015-12-31T16:00:23.446Z/PT1H",
  "is_schedule_active": true,
  "runtime_vars": {
    "DB_HOST": "localhost"
  }
}
```

##获得任务列表
`GET /v1/jobs?namespace=(namespace)`

**返回结果示例（status code：200）**

```json
{
  "count": 5,
  "previous": null,
  "results": [
    {
      "docker_image_repo": "index.alauda.cn/chennanfei/job_image",
      "name": "test2",
      "region_name": "BEIJING1",
      "created_at": "2015-12-28T14:31:07.639Z",
      "namespace": "chennanfei",
      "updated_at": "2015-12-28T14:41:05.672Z",
      "created_by": "chennanfei",
      "resource_size": "XS",
      "schedule_mode": null,
      "docker_image_tag": "trusty",
      "command": "/bin bash",
      "is_schedule_active": false,
      "id": 146,
      "runtime_vars": {
        "DB_HOST": "127.0.0.1"
      }
    },
    ...
  ],
  "next": null
}
```

##获得任务详情
```GET /v1/jobs/(job_id)```

**返回结果示例（status code：200）**

```json
{
  "id": 146,
  "docker_image_repo": "index.alauda.cn/chennanfei/job_image",
  "name": "test",
  "region_name": "BEIJING1",
  "created_at": "2015-12-28T14:31:07.639255+00:00",
  "namespace": "chennanfei",
  "updated_at": "2015-12-28T14:31:07.639296+00:00",
  "created_by": "chennanfei",
  "resource_size": "XXS",
  "schedule_mode": "R1/2015-12-31T16:00:23.446Z/PT1H",
  "docker_image_tag": "latest",
  "command": "bash",
  "is_schedule_active": true,
  "runtime_vars": {
    "DB_HOST": "localhost"
  }
}
```

##更新任务
`PUT /v1/jobs/(job_id)`

```json
{
  "name": "test2",
  "command": "/bin bash",
  "docker_image_tag": "trusty",
  "resource_size": "XS",
  "is_schedule_active": false,
  "schedule_mode": null,
  "runtime_vars": {
    "DB_HOST": "127.0.0.1"
  }
}
```

**返回结果示例（status code：200）**

```json
{
  "id": 146,
  "docker_image_repo": "index.alauda.cn/chennanfei/job_image",
  "name": "test2",
  "region_name": "BEIJING1",
  "created_at": "2015-12-28T14:31:07.639255+00:00",
  "namespace": "chennanfei",
  "updated_at": "2015-12-28T14:41:05.672783+00:00",
  "created_by": "chennanfei",
  "resource_size": "XS",
  "schedule_mode": null,
  "docker_image_tag": "trusty",
  "command": "/bin bash",
  "is_schedule_active": false,
  "runtime_vars": {
    "DB_HOST": "127.0.0.1"
  }
}
```

##删除任务
`DELETE /v1/jobs/(job_id)`

**返回结果示例（status code：204）**

##触发任务执行
`POST /v1/jobs/(job_id)/execs`

**返回结果示例（status code：201）**

```json
{
  "id": "64b2d045-2881-4293-9bcd-bdc04b953115",
  "job": 146,
  "docker_image_repo": "index.alauda.cn/chennanfei/job_image",
  "status": "W",
  "created_at": "2015-12-28T14:51:53.074169+00:00",
  "started_at": null,
  "ended_at": null,
  "runtime_vars": {
    "DB_HOST": "127.0.0.1"
  },
  "resource_size": "XS",
  "created_by": "chennanfei",
  "docker_image_tag": "trusty",
  "command": "/bin bash",
  "trigger_mode": "M",
  "duration": null,
  "region_name": "BEIJING1"
}
```

##获得任务执行记录列表
`GET /v1/jobs/(jobs_id)/execs`

**返回结果示例（status code：200）**

```json
{
  "count": 2,
  "previous": null,
  "results": [
    {
      "id": "64b2d045-2881-4293-9bcd-bdc04b953115",
      "job": 146,
      "docker_image_repo": "index.alauda.io/chennanfei/job_image",
      "status": "F",
      "ended_at": "2015-12-28T14:52:12.952491+00:00",
      "runtime_vars": {
        "DB_HOST": "127.0.0.1"
      },
      "created_at": "2015-12-28T14:51:53.074169+00:00",
      "resource_size": "XS",
      "created_by": "chennanfei",
      "docker_image_tag": "trusty",
      "command": "/bin bash",
      "trigger_mode": "M",
      "duration": {
        "hours": 0,
        "seconds": 10,
        "minutes": 0
      },
      "started_at": "2015-12-28T14:52:02.952491+00:00",
      "region_name": "BEIJING1"
    },
    ...
  ],
  "next": null
}
```

##获得任务执行记录详情
`GET /v1/jobs/(job_id)/execs/(exec_id)`


**返回结果示例（status code：200）**

```json
{
  "docker_image_repo": "index.alauda.io/chennanfei/job_image",
  "status": "F",
  "ended_at": "2015-12-28T14:52:12.952491+00:00",
  "runtime_vars": {
    "DB_HOST": "127.0.0.1"
  },
  "created_at": "2015-12-28T14:51:53.074169+00:00",
  "resource_size": "XS",
  "created_by": "chennanfei",
  "job": {
    "docker_image_repo": "index.alauda.io/chennanfei/job_image",
    "name": "test2",
    "region_name": "BEIJING1",
    "created_at": "2015-12-28T14:31:07.639255+00:00",
    "namespace": "chennanfei",
    "updated_at": "2015-12-28T14:41:05.672783+00:00",
    "created_by": "chennanfei",
    "resource_size": "XS",
    "schedule_mode": null,
    "docker_image_tag": "trusty",
    "command": "/bin bash",
    "email_enabled": false,
    "is_schedule_active": false,
    "id": 146,
    "runtime_vars": "{\"DB_HOST\": \"127.0.0.1\"}"
  },
  "docker_image_tag": "trusty",
```

##删除任务执行记录
`DELETE /v1/jobs/(job_id)/execs/(exec_id)`

**返回结果示例（status code：204）**


##任务Web钩子
创建任务的Web钩子请参考[Web钩子](webhook.md)
