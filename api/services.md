## 创建服务
`POST /v1/services/(namespace)`

**请求示例**:
```json
{
    "service_name": "test",
    "namespace": "madams",
    "application": "app_name_or_null",
    "image_name": "index.alauda.cn/alauda/ubuntu",
    "image_tag": "latest",
    "run_command": "",
    "instance_size": "XS",
    "scaling_mode": "MANUAL",
    "target_state": "STARTED",
    "custom_domain_name": "my-own-domain.cn",
    "target_num_instances": 2,
    "instance_envvars":{
        "POSTGRES_USER":"root",
        "POSTGRES_PASSWORD":"123456",
        "PG_HOST": "127.0.0.1",
        "PG_PORT": "5432",
        "REPO_NAME": "pypg2",
        "FILENAME": "scale_with_db"
    },
    "instance_ports":[
        {
            "container_port": 22,
            "protocol": "tcp",
            "endpoint_type": "tcp-endpoint"
        },
        {
            "container_port": 22,
            "protocol": "tcp",
            "endpoint_type": "direct-endpoint"
        }
    ],
    "autoscaling_config": {
        "metric_name" : "CPU_UTILIZATION",
        "metric_stat" : "MEAN",
        "upper_threshold" : "0.6",
        "lower_threshold" : "0.1",
        "decrease_delta" : "1",
        "increase_delta" : "1",
        "minimum_num_instances" : "1",
        "maximum_num_instances" : "6",
        "wait_period" : "30"
    },
    "volumes" : [
        {
            "app_volume_dir" : "/data1",
            "volume_type" : "EBS",
            "size_gb" : 10
        },
        {
            "app_volume_dir" : "/data2",
            "volume_type" : "EBS",
            "size_gb" : 20
        }
    ]
}
```

参数:

* **service_name**: - 服务名称，在每个用户创建的服务中必须唯一。后面某些API中的app_name和这个是一个含义。
* **namespace**: 服务所属用户名或机构名
* **run_command**: 运行docker时执行的命令
* **image_name** 服务使用的镜像
* **image_tag** 服务使用的镜像版本
* **instance_size**: 容器实例大小，可选项为：“XS”，“S”，“M”，“L”，“XL”
* **scaling_mode**: 调节模式，只对无状态服务有效。可选项为：“MANUAL”，“AUTO”
* **target_state**: 服务创建后的目标状态，可选项为：“STARTED”，“STOPPED”
* **custom_domain_name**: 用户自定义的域名，目前能设置一个域名，如“www.myname.com”
* **linked_to_apps** 该服务要连接的其它服务
* **target_num_instances**: 服务的实例数量
* **instance_envvars**: 环境变量
* **instance_ports**: 端口设置
* **autoscaling_config**: 当选择自动调节模式时的参数配置
* **volumes**: 存储卷
* **application**: 所属应用名称


## 服务列表
`GET /v1/services/(namespace)`



**返回示例**:
```json
{
    "count": 2,
    "previous": null,
    "results": [
        {
            "unique_name": "1cd688e2-b4eb-4bf8-9113-5caccdec2db6",
            "service_name": "test",
            "namespace": "madams",
            "updated_at": "2015-04-14T09:46:39.457Z",
            "allocation_group": null,
            "target_state": "STARTED",
            "instance_envvars": "{}",
            "started_at": null,
            "uuid": "1cd688e2-b4eb-4bf8-9113-5caccdec2db6",
            "linked_to_apps": "{}",
            "stopped_at": null,
            "is_deploying": false,
            "created_by": "madams",
            "autoscaling_config": "{}",
            "instance_ports": {},
            "linked_to": "{}",
            "run_command": "",
            "custom_domain_name": "my-own-domain.cn",
            "deployment_preference": "{}",
            "scaling_mode": "MANUAL",
            "image_name": "index.alauda.cn/alauda/ubuntu",
            "image_tag": "latest",
            "instance_size": "XS",
            "linked_from_apps": "{}",
            "target_num_instances": 1,
            "last_autoscaled_at": null,
            "current_num_instances": 1,
            "linked_from": "{}",
            "staged_num_instances": 0,
            "started_num_instances": 1,
            "instances": [
                {
                    "instance_name": "test.0",
                    "started_at": "2015-04-14T09:47:26.895Z",
                    "uuid": "92d03b63-e34b-11e4-9fa4-0240eaf5c02d"
                }
            ],
            "created_at": "2015-04-14T09:46:39.457Z",
            "volumes": [],
            "default_domain_name": "test-madams.alaudacn.me",
            "resource_uri": "/api/v1/apps/test"
        },
        {
            "unique_name": "0cae164e-610c-4a2c-9d36-ff7d2f70054a",
            "service_name": "test1",
            "namespace": "madams",
            "updated_at": "2015-04-14T09:47:09.623Z",
            "target_state": "STARTED",
            "instance_envvars": "{}",
            "started_at": null,
            "uuid": "0cae164e-610c-4a2c-9d36-ff7d2f70054a",
            "linked_to_apps": "{}",
            "stopped_at": null,
            "is_deploying": false,
            "namespace": "madams",
            "created_by": "madams",
            "autoscaling_config": "{}",
            "instance_ports": {},
            "linked_to": "{}",
            "run_command": "",
            "custom_domain_name": "my-own-domain.cn",
            "deployment_preference": "{}",
            "scaling_mode": "MANUAL",
            "image_name": "tutum/ubuntu",
            "image_tag": "latest",
            "instance_size": "XS",
            "linked_from_apps": "{}",
            "target_num_instances": 1,
            "last_autoscaled_at": null,
            "current_num_instances": 1,
            "linked_from": "{}",
            "staged_num_instances": 0,
            "started_num_instances": 1,
            "instances": [
                {
                    "instance_name": "test1.0",
                    "started_at": "2015-04-14T09:47:26.895Z",
                    "uuid": "dcdaadc3-82a6-4ec1-9baa-58f35713626"
                }
            ],
            "created_at": "2015-04-14T09:47:09.623Z",
            "volumes": [
                {
                    "app_volume_dir": "/data/config",
                    "size_gb": 10
                }
            ],
            "default_domain_name": "test1-madams.alaudacn.me",
            "resource_uri": "/api/v1/apps/test1"
        }
    ],
    "next": null
}
```

参数:

* **count** 用户已经创建的服务个数
* **previous**
* **unique_name**: - 服务的唯一标示符。遵从如下的正则表达式规则:

    `^(([a-z0-9]|[a-z0-9][a-z0-9\-][a-z0-9])\.)([a-z0-9]|[a-z0-9][a-z0-9\-]*[a-z0-9])$`

* **updated_at** 最后更新时间
* **allocation_group** 专属VM标记
* **started_at** 启动时间
* **stopped_at** 停止时间
* **is_deploying** 是否正在部署中
* **namespace** 服务所属用户名或机构名
* **created_by** 创建者




## 获取服务信息

`GET /v1/services/(namespace)/(service_name)/`


**返回示例**:
```json
{
    "unique_name": "1cd688e2-b4eb-4bf8-9113-5caccdec2db6",
    "service_name": "test",
    "updated_at": "2015-04-14T09:46:39.457Z",
    "target_state": "STARTED",
    "instance_envvars": "{}",
    "started_at": null,
    "linked_to_apps": "{}",
    "stopped_at": null,
    "is_deploying": false,
    "namespace": "madams",
    "created_by": "madams",
    "autoscaling_config": "{}",
    "instance_ports": {},
    "linked_to": "{}",
    "run_command": "",
    "custom_domain_name": "my-own-domain.cn",
    "deployment_preference": "{}",
    "scaling_mode": "MANUAL",
    "image_name": "index.alauda.cn/alauda/ubuntu",
    "linked_from_apps": "{}",
    "target_num_instances": 1,
    "last_autoscaled_at": null,
    "current_num_instances": 1,
    "linked_from": "{}",
    "staged_num_instances": 0,
    "started_num_instances": 1,
    "instances": [
        {
            "instance_name": "test.0",
            "started_at": "2015-04-14T09:49:56.141Z",
            "uuid": "dcdaadc3-82a6-4ec1-9baa-58f35713626"
        }
    ],
    "created_at": "2015-04-14T09:46:39.457Z",
    "volumes": [],
    "default_domain_name": "test-madams.alaudacn.me",
    "image_tag": "latest",
    "instance_size": "XS",
    "resource_uri": "/api/v1/apps/test"
}
```


## 更新服务
`PUT /v1/services/(namespace)/(service-name)/`

更新某个服务的参数，比如调整其实例个数

**请求示例**:
```json
{
    "service_name": "test",
    "target_num_instances": 3,
    "image_tag":"latest",
    "scaling_mode": "MANUAL"
}
```

## 启动服务
`PUT /v1/services/(namespace)/(service-name)/start/`

## 停止服务
`PUT /v1/services/(namespace)/(service-name)/stop/`

## 删除服务
`DELETE /v1/services/(namespace)/(service-name)/`

## 获取服务日志
`GET /v1/services/(namespace)/(service-name)/logs/`

**请求示例**:

`/v1/services/madams/test/logs?start_time=1433753210&end_time=1433753270`


**返回示例**:

```json
[
    {
        "instance_id": "a9aff249",
        "message": "172.31.14.54 - - [12/May/2015 08:47:36] \"GET /alauda.jpg HTTP/1.1\" 200 -",
        "time": 1433753256
    },
    {
        "instance_id": "a9afcb38",
        "message": "172.31.14.54 - - [12/May/2015 08:47:40] \"GET / HTTP/1.1\" 200 -",
        "time": 1433753260
    }
]
```

参数:
- **start_time** **end_time** 时间戳
- **instance_id** 产生日志的容器实例id
- **message** 日志内容
- **time** 日志创建的时间

