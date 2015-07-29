### 创建备份

`POST /v1/backups/(namespace)`

**请求示例**:
```json
{
    "app_id" : "24fc2fcc-d86a-4566-8476-bf5f264fa62b",
    "app_volume_dir" : "/data",
    "name" : "mysql-snapshot"     
}
```



**返回示例**:
```json
{
    "namespace": "madams"
    "status": "creating",
    "backup_id": "c38dc200-f8d5-4716-9dc4-9e4aed8cc5aa",
    "name": "mysql-snapshot",
    "created_datetime": "2015-03-08T10:00:17Z"
}
```


## 备份列表

`GET /v1/backups/(namespace)`

列出某个用户的所有备份信息

**返回示例**:
```json
[
    {
        "backup_id" : "8b1103a6-9023-421e-9289-70c3f9a0699f",
        "namespace" : "demo_user",
        "name" : "mysql-snapshot",
        "size_byte" : 1024,
        "created_datetime" :  "2011-07-14T19:43:37+0100",
        "status" : "available",
        "download_url": "http://xxxxxxxx",
        "error" : {
            "code" : "",
            "message" : ""        
        }
    }
]
```

## 备份信息

`GET /v1/backups/(namespace)/(backup_id)`

获取某个备份的详细信息

**返回示例**:
```json
{
    "backup_id" : "8b1103a6-9023-421e-9289-70c3f9a0699f",
    "namespace" : "demo_user",
    "name" : "mysql-snapshot",
    "size_byte" : 1024,
    "created_datetime" :  "2011-07-14T19:43:37+0100",
    "status" : "available",
    "download_url": "http://xxxxxxxx",
    "error" : {
        "code" : "",
        "message" : ""        
    }
}
```
