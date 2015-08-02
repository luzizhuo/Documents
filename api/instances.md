## 实例列表
`GET /v1/services/(namespace)/(service-name)/instances`

获取某个服务的实例列表

**返回示例**:
```json
[
    {
        "instance_name": "test.0",
        "uuid": "1cd688e2-b4eb-4bf8-9113-5caccdec2db6",
        "started_at": "2015-03-19T03:56:04.095Z"
    },
    {
        "instance_name": "test.1",
        "uuid": "dcdaadc3-82a6-4ec1-9baa-58f35713626",
        "started_at": "2015-03-19T03:56:04.095Z"
    }
]
```

## 实例信息

`GET /v1/services/(namespace)/(service-name)/instances/(instance-uuid)/`

获取某个实例的详细信息

**返回示例**:
```json
{
    "instance_name": "test.1",
    "uuid": "79fe9743-cdda-11e4-b3e7-0240eaf5c02d",
    "started_at": "2015-03-19T01:51:36.126Z"
}
```

## 实例日志

`GET /v1/services/(namespace)/(service-name)/instances/(instance-uuid)/logs`

获取某个实例的日志信息

**请求示例**:

`/v1/services/madams/test/instances/1cd688e2-b4eb-4bf8-9113-5caccdec2db6/logs?start_time=1433753210&end_time=1433753270`

**返回示例**:
```json
[
    {
        "message": "172.31.14.54 - - [12/May/2015 08:47:40] \"GET / HTTP/1.1\" 200 -"
    },
    {
        "message": "172.31.14.54 - - [12/May/2015 08:47:41] \"GET /favicon.ico HTTP/1.1\" 200 -"
    }
]
```


## 实例运行时信息:
`GET /v1/services/(namespace)/(service-name)/instances/(instance-uuid)/metrics`

获取某个实例的运行时信息

**请求示例**:

`/v1/services/madams/test/instances/a9afcb38-0db5-11e5-a6be-02416b28d26a/metircs?start_time=1433753087&end_time=1433753090&point_per_period=1m`

参数:

* **point_per_period** -  可以为 “1s”, “1m”, “5m”, “15m”, “30m”, “1h”, “4h”, “12h”, “1d”, “7d”, “30d”.


**返回示例**:
```json
{
    "name": "stats.0f598d55_8bf0_4c7b_9388_5457a1ec0228.a9afcb38_0db5_11e5_a6be_02416b28d26a",
    "columns": [
        "time",
        "sequence_number",
        "cpu_cumulative_usage",
        "cpu_utilization",
        "memory_usage",
        "memory_utilization",
        "rx_bytes",
        "rx_errors",
        "tx_bytes",
        "tx_errors"
    ],
    "points": [
        [
            1433753089,
            0,
            310527696,
            0.012714308333173054,
            16072704,
            2.9937744140625,
            84560,
            0,
            45786,
            0
        ],
        [
            1433753088,
            0,
            310428354,
            0.012715614990320428,
            16072704,
            2.9937744140625,
            84560,
            0,
            45786,
            0
        ],
        [
            1433753087,
            0,
            310327527,
            0.01271685307576187,
            16072704,
            2.9937744140625,
            84560,
            0,
            45786,
            0
        ]
    ]
}
```


参数:

- **columns**
- **points**
