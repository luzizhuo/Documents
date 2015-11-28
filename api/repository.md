## 创建镜像仓库

`POST /v1/repositories/(namespace)/`

**请求示例**:
```json
{
    "repo_name": "repo",
    "description": "A repo docker image repository",
    "namespace": "madams",
    "is_public": true
}
```

参数:
- **repo_name** 镜像仓库名称
- **namespace** 镜像仓库所属的用户名或机构名
- **is_public** 镜像仓库是否为公共的
- **description** 镜像仓库描述




**返回示例**:
```json
{
    "repo_name": "repo",
    "namespace": "madams",
    "repo_path": "madams/repo",
    "is_automated": False,
    "description": "A repo docker image repository",
    "creation_time": "2014-11-19T05:54:22.741Z",
    "updated_time": "2014-11-19T05:54:22.741Z",
    "is_public": true,
    "logo": "default-icon.jpg"
}
```

参数:

- **is_automated** 是否镜像构建仓库



## 镜像仓库列表:

`GET /v1/repositories/(namespace)/`


列出某个用户的所有镜像仓库

**返回示例**:
```json
{
    "count":  3,
    "next": null,
    "previous": null,
    "results": [
        {
            "repo_name": "repo1",
            "namespace": "madams",
            "repo_path": "madams/repo1",
            "is_automated": False,
            "description": "repo1",
            "creation_at": "2014-11-19T05:54:22.741Z",
            "updated_at": "2014-11-19T05:54:22.741Z",
            "is_public": true,
            "logo": "default-icon.jpg",
            "repo_starred_count": 0,
            "full_description": "",
            "download": 0,
            "upload": 9,
            "pulled_at": null,
            "pushed_at": "2015-06-04T16:30:27.532Z"
        },
        {
            "repo_name": "repo2",
            "namespace": "madams",
            "repo_path": "madams/repo2",
            "is_automated": False,
            "description": "repo2",
            "creation_at": "2014-11-19T05:55:42.741Z",
            "updated_at": "2014-11-19T05:55:42.741Z",
            "is_public": true,
            "logo": "default-icon.jpg"
            "repo_starred_count": 0,
            "full_description": "",
            "download": 0,
            "upload": 9,
            "pulled_at": null,
            "pushed_at": "2015-06-04T16:30:27.532Z"
        }
    ]
}
```

## 更新镜像仓库:

`PUT /v1/repositories/(namespace)/(repo-name)`


**返回示例**:
```json
{
    "repo_name": "repo",
    "namespace": "madams",
    "repo_path": "madams/repo",
    "description": "A repo docker image repository",
    "is_public": true,
    "logo": "default-icon.jpg"
}
```

## 镜像仓库信息

`GET /v1/repositories/(namespace)/(repo-name)`

获取某个镜像仓库的详细信息

**返回示例**:
```json
{
    "namespace": "madams",
    "repo_name": "test",
    "repo_path": "madams/test",
    "logo_file": "/static/images/user/default-logo.png",
    "description": "test",
    "full_description": "test contain 2 tags",
    "repo_starred_count": 0,
    "created_at": "2015-05-13T01:04:48.246Z",
    "updated_at": "2015-06-07T10:41:31.882Z",
    "is_public": false,
    "logo": "default-icon.jpg",
    "is_automated": false,
    "download": 103,
    "upload": 4,
    "pulled_at": "2015-06-07T10:41:31.881Z",
    "pushed_at": "2015-05-24T00:54:26.452Z",
    "is_repo_starred": false
}
```

## Tags列表

`GET /v1/repositories/(namespace)/(repo-name)/tags`

获取某个镜像仓库的`Tags`列表

**返回示例**:
```json
[
    {
        "image_id": "a4002247cb22e78c8d9ffeccdf7ea23d7763f53493d4d763cb4dbe58bf3566b5",
        "tag": "test"
    },
    {
        "image_id": "e72ac664f4f0c6a061ac4ef332557a70d69b0c62fb6add35f1c181ff7fff2287",
        "tag": "latest"
    }
]
```

## 删除 Tag

`DELETE /v1/repositories/(namespace)/(repo-name)/tags/(tag)`

删除某个镜像仓库下的某个`Tag`


## 删除镜像源

`DELETE /v1/repositories/(namespace)/(repo-name)/`


