## Create Service
`POST /v1/services/(namespace)`

Create and start a new service.

**Example Request**:
```json
{
    "service_name": "test",
    "namespace": "madams",
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

Query Parameters:

* **service_name**: - the name of the service. It must be unique among the services created by the requesting user.
* **state**: - the state of the service.


## List services
`GET /v1/services/(namespace)`

List all services.

**Example Request**:
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

Query Parameters:

* **unique_name**: - unique identifier for the service consisting of a series of names separated by slashes. Each name must be at least 1 character and may only contain digits (0-9), dashes (-), and lowercase letters (a-z). The name may not begin or end with a dash. The allowable format is represented by the following regular expression:
  `^(([a-z0-9]|[a-z0-9][a-z0-9\-][a-z0-9])\.)([a-z0-9]|[a-z0-9][a-z0-9\-]*[a-z0-9])$`



