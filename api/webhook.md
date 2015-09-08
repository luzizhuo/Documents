##创建Web钩子

`POST /v1/hooks`

```json
{
	"subject_type": "build_repo",
	"subject": "alaudauser/docker_images_test",
	"events": ["build:complete"],
	"secret": "123456",
	"url": "http://example.com:8080/v1/builds",
	"name": "test hook"
}
```

**参数说明**

- **subject_type**：可以选build_repo（镜像构建仓库）、image_repo（镜像仓库）

- **subject**：镜像（构建）仓库的短路经（由命名空间和仓库名组成）

- **events**：事件集合

- **secret**：密钥，用作计算数字签名

- **url**：Web钩子的回调URL

- **name**：Web钩子的名称

**返回结果示例（status code：201）**

```json
{
	"id": 4,
	"subject": "alaudauser/build_image_demo",
    "subject_type": "build_repo",
    "events": [
        "build:complete"
    ],
    "name": "test hook",
    "secret": "123456",
    "url": "http://example.com:8080/v1/builds",
    "is_active": true,
    "created_by": "alaudauser",
    "created_at": "2015-08-27T09:53:43.563Z",
    "updated_at": "2015-08-27T09:53:43.566Z"
}
```

##获得钩子列表

`GET /v1/hooks?subject_type=<subject_type>&subject=<subject>`

**返回结果示例（status code：200）**

```json
[
    {
        "id": 4,
        "subject": "alaudadoc/docker_images_test",
        "subject_type": "build_repo",
        "events": [
            "build:complete"
        ],
        "name": "test hook",
        "secret": "123456",
        "url": "http://www.example.com:8080/v1/builds",
        "is_active": true,
        "created_by": "alaudadoc",
        "created_at": "2015-08-27T09:53:43.563Z",
        "updated_at": "2015-08-27T09:53:43.566Z"
    },
    {
       …
       …
    }
]
```

##获得钩子详情

`GET /v1/hooks/<hook_id>`

** 返回结果示例（status code：200）**

```json
{
    "id": 4,
    "subject": "alaudadoc/docker_images_test",
    "subject_type": "build_repo",
    "events": [
        "build:complete"
    ],
    "name": "test hook",
    "secret": "123456",
    "url": "http://www.example.com:8080/v1/builds",
    "is_active": true,
	"created_by": "alaudadoc",
	"created_at": "2015-08-27T09:53:43.563Z",
   	"updated_at": "2015-08-27T09:53:43.566Z"
}
```

##更新Web钩子

`PUT /v1/hooks/<hook_id>`

```json
{
	"events": ["build:complete"],
	"secret": "alaudadoc",
	"url": "http://www.example.com:8080/v1/builds",
	"name": "build hook",
	"is_active": false
}
```

**返回结果示例（status code：200）**

```json
{
    "id": 4,
    "subject": "alaudadoc/docker_images_test",
    "subject_type": "build_repo",
    "events":
   	[
   	    "build:complete"
    ],
    "name": "build hook",
    "secret": "alaudadoc",
    "url": "http://www.example.com:8080/v1/builds",
    "is_active": true,
    "created_by": "alaudadoc",
    "created_at": "2015-08-27T09:53:43.563Z",
    "updated_at": "2015-08-27T10:02:42.436Z"
}
```

##删除Web钩子

`DELETE /v1/hooks/<hook_id>`

**返回结果示例（status code：204）**

