## 创建应用

`POST v1/applications/<namespace>/<app-name>/`

`Content-Type: multipart/form-data;boundary="simple boundary`


**请求示例**:
```json
$ curl -H "Authorization:Token your-token" -H "Content-Type: multipart/form-data; boundary=simple boundary" -F "app_name=test" -F "region=BEIJING12" -F "services=@docker-compose.yml" 'https://api.alauda.cn/v1/applications/madams/'
```


参数:

* **app_name**: - 应用名称，在每个用户创建的应用中必须唯一。
* **namespace**: 应用所属用户名或机构名
* **region**:应用所属区，有BEIJING1, BEIJING2, SHANGHAI1, HONGKONG1
* **services** 应用的编排文件



## 应用列表
`GET /v1/applications/(namespace)`


**返回示例**:
```json
[
  {
    "id": 1,
    "services": [
      {
        "unique_name": "1721d3e9-3980-45c2-b4fb-75e401234567",
        "app_name": "redis",
        "service_name": "redis",
        "updated_at": "2015-11-06T07:21:03.591Z",
        "allocation_group": null,
        "target_state": "STOPPED",
        "instance_envvars": "{\"__DEFAULT_DOMAIN_NAME__\": \"redis-madams.myalauda.cn\"}",
        "current_status": "Stopped",
        "started_at": null,
        "last_redeployed_at": "2015-11-06T07:21:03.556Z",
        "linked_services": [],
        "uuid": "1721d3e9-3980-45c2-b4fb-75e403a3f297",
        "linked_to_apps": "{}",
        "stopped_at": null,
        "namespace": "madams",
        "created_by": "madams",
        "application": "test",
        "autoscaling_config": "{\"increase_delta\": 1, \"maximum_num_instances\": 5, \"metric_name\": \"CPU_UTILIZATION\", \"decrease_delta\": 1, \"upper_threshold\": \"0.95\", \"lower_threshold\": \"0.5\", \"wait_period\": 120, \"metric_stat\": \"MEAN\", \"minimum_num_instances\": 2}",
        "instance_ports": [
          {
            "protocol": "tcp",
            "container_port": 6379
          }
        ],
        "linked_to": "{}",
        "run_command": "",
        "custom_domain_name": "",
        "linked_to_services": [],
        "deployment_preference": "{}",
        "scaling_mode": "MANUAL",
        "image_name": "redis",
        "linked_from_apps": "{}",
        "region": {
          "IaaS": "AWS",
          "name": "BEIJING12"
        },
        "target_num_instances": 1,
        "last_autoscaled_at": null,
        "linked_from": "{}",
        "created_at": "2015-11-06T07:21:03.591Z",
        "not_exist": true,
        "exec_endpoint": "exec.alauda.cn",
        "volumes": [],
        "default_domain_name": "redis-madams.myalauda.cn",
        "image_tag": "latest",
        "instance_size": "XS",
        "resource_uri": "/api/v1/apps/redis"
      },
    ],
    "app_name": "test",
    "region": "BEIJING12",
    "namespace": "madams",
    "created_by": "madams",
    "current_status": "Stopped"
  },
]
```



## 获取应用信息

`GET /v1/applications/(namespace)/(app-name)/`


**返回示例**:
```json
{
  "id": 1,
  "services": [
    {
      "unique_name": "1721d3e9-3980-45c2-b4fb-75e401234567",
      "app_name": "redis",
      "service_name": "redis",
      "updated_at": "2015-11-06T07:21:03.591Z",
      "allocation_group": null,
      "target_state": "STOPPED",
      "instance_envvars": "{\"__DEFAULT_DOMAIN_NAME__\": \"redis-madams.myalauda.cn\"}",
      "current_status": "Stopped",
      "started_at": null,
      "last_redeployed_at": "2015-11-06T07:21:03.556Z",
      "linked_services": [],
      "uuid": "1721d3e9-3980-45c2-b4fb-75e403a3f297",
      "linked_to_apps": "{}",
      "stopped_at": null,
      "namespace": "madams",
      "created_by": "madams",
      "application": "test",
      "autoscaling_config": "{\"increase_delta\": 1, \"maximum_num_instances\": 5, \"metric_name\": \"CPU_UTILIZATION\", \"decrease_delta\": 1, \"upper_threshold\": \"0.95\", \"lower_threshold\": \"0.5\", \"wait_period\": 120, \"metric_stat\": \"MEAN\", \"minimum_num_instances\": 2}",
      "instance_ports": [
        {
          "protocol": "tcp",
          "container_port": 6379
        }
      ],
      "linked_to": "{}",
      "run_command": "",
      "custom_domain_name": "",
      "linked_to_services": [],
      "deployment_preference": "{}",
      "scaling_mode": "MANUAL",
      "image_name": "redis",
      "linked_from_apps": "{}",
      "region": {
        "IaaS": "AWS",
        "name": "BEIJING12"
      },
      "target_num_instances": 1,
      "last_autoscaled_at": null,
      "linked_from": "{}",
      "created_at": "2015-11-06T07:21:03.591Z",
      "not_exist": true,
      "exec_endpoint": "exec.alauda.cn",
      "volumes": [],
      "default_domain_name": "redis-madams.myalauda.cn",
      "image_tag": "latest",
      "instance_size": "XS",
      "resource_uri": "/api/v1/apps/redis"
    },
  ],
  "app_name": "test",
  "region": "BEIJING12",
  "namespace": "madams",
  "created_by": "madams",
  "current_status": "Stopped"
}
```



## 获取应用编排文件

`GET /v1/applications/(namespace)/(app-name)/yaml/`



## 启动应用
`PUT /v1/applications/(namespace)/(app-name)/start/`



## 停止应用
`PUT /v1/applications/(namespace)/(app-name)/stop/`



## 删除应用
`DELETE /v1/applications/(namespace)/(app-name)/`

