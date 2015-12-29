## 创建镜像构建仓库

`POST /v1/repositories/(namespace)`

**请求示例**:

```json
{
    "repo_name": "docker_images_test",
    "description": "docker images",
    "full_description": "",
    "is_public": true,
    "build_config": {
        "code_repo_client": "GitHub",
        "code_repo_namespace": "yournamespace",
        "code_repo_name": "Docker-image",
        "build_node": "in",
        "email_enabled": false,
        "tag_configs": [
            {
				"code_repo_type": "branch",
				"code_repo_type_value": "master",
				"docker_repo_tag": "latest",
				"build_context_path": "/",
				"dockerfile_location": "/",
				"is_active": false,
				"version_tagging": 1
            }
        ]
    }
}
```

参数:

- **repo_name** 镜像构建仓库的仓库名称
- **description** 镜像构建仓库的简要描述
- **full_description** 镜像构建仓库的详细描述
- **is_public** 是否为公有的镜像构建仓库
- **code_repo_client** 可选择`GitHub`, `Bitbucket`, `OSChina`, `GitCafe`, `Simple`
	若选择Simple, build config 需为:

	"build_config": {
        "code_repo_client": "Simple",
        "code_repo_clone_url": "http://github.com/example/example.git",
        "tag_configs": [
            {
                "code_repo_type": "branch",
 	   			"code_repo_type_value": "master",
                "docker_repo_tag": "latest",
                "dockerfile_location": "/",
                "is_active": false,
                "version_tagging": 1
            }
        ]
    }
    
- **code_repo_namespace** 代码仓库源的用户或组名
- **code_repo_name** 对应选择的代码仓库源的项目名称
- **code_repo_type** 为branch或tag
- **docker_build_tag** 构建的版本标记
- **dockerfile_location** dockerfile的路径
- **is_active** 如果需要开启持续构建
- **version_tagging** 设置为0，不会生成附加版本标记；设置为1，附加时间版本标记；设置为2，生成一个代码变更id作为附加版本标记


**返回示例**:
```json
{
    "repo_starred_count": 0,
    "namespace": "alauda",
    "logo_file": "/static/images/user/default-logo.png",
    "repo_path": "alauda/docker_images_test",
    "repo_name": "docker_images_test",
    "description": "docker images",
    "full_description": "",
    "created_by": "alauda",
    "created_at": "2015-09-02T08:37:13.728Z",
    "updated_at": "2015-09-02T08:37:13.728Z",
    "is_public": true,
    "is_automated": true,
    "download": 0,
    "upload": 0,
    "pulled_at": null,
    "pushed_at": null,
    "build_config": {
        "id": 3,
        "docker_repo_path": "alauda/docker_images_test",
        "code_repo_client": "GitHub",
        "code_repo_path": "alauda/testtest",
        "code_repo_webhook_code": null,
        "code_repo_public_key": "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAAAgQCIQ/0AIGT2Vzu7V9XTuA2O9mFLY7y7IQICdvf7ul08B6Z1SBQnLnnP1/LPyKGBaNGVDC0YM/pFFp+FqLCpaDyzQh3u1oMbL4wlmbCsOh5vt7YHEU5Rm2oLxen/TPICHWSVhGYY/m6hybtz+vebPuSLRctHNGuDYRV9Xqru+SdULw==",
        "created_by": "alauda",
        "build_node": "in",
        "email_enabled": false,
        "code_repo_path_url": "https://github.com/alauda/testtest",
        "deploy_url": "https://github.com/alauda/testtest/settings/keys",
        "tag_configs": [
            {
                "id": 4,
                "docker_build_config_id": 3,
                "docker_repo_tag": "latest",
                "dockerfile_location": "/",
                "code_repo_type": "branch",
                "code_repo_type_value": "master",
                "is_active": false,
                "version_tagging": 1,
                "build_context_path": "/"
            }
        ]
    }
}
```

## 获得构建的记录

`GET /v1/builds?namespace=(namespace)&page=(page)&repo_name=(repo_name)`

参数:

- **namespace(optional)** 默认返回当前用户的构建
- **page(optional)** 默认为1，每页最多20个构建记录
- **repo_name(optional)** 获得当前repo_name下的构建记录

**返回示例**:
```json
{
    "count": 60,
    "next": "https://api.alauda.cn/v1/builds?page=3",
    "previous": "https://api.alauda.cn/v1/builds?page=1",
    "results": [
        {
            "build_id": "a3865a8e-f3d2-47a5-8ff1-80c714f89d4b",
            "created_at": "2015-05-28T11:13:27.146Z",
            "started_at": "2015-05-28T11:13:20.792Z",
            "ended_at": "2015-05-28T11:19:08.950Z",
            "code_head_commit": "119d9dc6f33992b6c4f8ddf068e347d426ddf22c",
            "code_repo_client": "Bitbucket",
            "code_repo_path": "mathildetech/ms-aspnet",
            "code_repo_type": "branch",
            "code_repo_type_value": "master",
            "created_by": "chennanfei",
            "detail": "build request was created.\n",
            "image_id": "16db7a76b5cf",
            "docker_repo_path": "chennanfei/ms-aspnet",
            "docker_repo_tag": "latest",
            "docker_repo_version_tag": "v20150528.111327",
            "dockerfile_location": "/",
            "status": "S",
            "auto_created": false,
            "code_repo_http_url": "https://bitbucket.org/mathildetech/ms-aspnet",
            "code_commit_http_url": "https://bitbucket.org/mathildetech/ms-aspnet/commits/119d9dc6f33992b6c4f8ddf068e347d426ddf22c",
            "code_repo_branch_url": "https://bitbucket.org/mathildetech/ms-aspnet/branch/master"
        },
        {
            "build_id": "178cad9d-49eb-4ac1-b052-a5ea41c36c45",
            "created_at": "2015-05-28T03:21:41.051Z",
            "started_at": "2015-05-28T03:21:35.971Z",
            "ended_at": "2015-05-28T03:22:59.997Z",
            "code_head_commit": "2980b75621712dd986e4a006cb62adc5e96064b1",
            "code_repo_client": "Bitbucket",
            "code_repo_path": "mathildetech/ms-aspnet",
            "code_repo_type": "branch",
            "code_repo_type_value": "master",
            "created_by": "chennanfei",
            "detail": "build request was created.\n",
            "image_id": "1f129b14e4db",
            "docker_repo_path": "chennanfei/ms-aspnet",
            "docker_repo_tag": "latest",
            "docker_repo_version_tag": "v20150528.032141",
            "dockerfile_location": "/",
            "status": "S",
            "auto_created": false,
            "code_repo_http_url": "https://bitbucket.org/mathildetech/ms-aspnet",
            "code_commit_http_url": "https://bitbucket.org/mathildetech/ms-aspnet/commits/2980b75621712dd986e4a006cb62adc5e96064b1",
            "code_repo_branch_url": "https://bitbucket.org/mathildetech/ms-aspnet/branch/master"
        }
        ...
]
```

## 触发构建

`POST /v1/builds`

**请求示例**:
```json
{
    "namespace": "alauda",
    "repo_name": "test",
    "tag": "latest",
    "code_commit_id": "552819d5c903472a36696e8ac620ac250e49829d"
}
```

参数:

- **namespace** 当前用户或组名
- **repo_name** 镜像构建仓库名
- **tag** 指定构建的目标版本
- **code_commit_id(optional)** 代码变更id

**返回示例**:
```json
{
    "build_id": "5709f780-e8fb-4b52-aa3b-6256b572fb51",
    "created_at": "2015-09-02T08:17:42.581Z",
    "started_at": null,
    "ended_at": null,
    "code_head_commit": "552819d5c903472a36696e8ac620ac250e49829d",
    "code_repo_client": "Bitbucket",
    "code_repo_path": "alauda/buildtest",
    "code_repo_type": "branch",
    "code_repo_type_value": "master",
    "created_by": "alaudatest",
    "image_id": null,
    "docker_repo_path": "alauda/buildtes34t",
    "docker_repo_tag": "latest",
    "docker_repo_version_tag": "v20150902.081742",
    "dockerfile_location": "/",
    "status": "W",
    "auto_created": false,
    "step_at": 1,
    "build_node": "in",
    "build_context_path": "/",
    "code_repo_http_url": "https://bitbucket.org/yingdai/buildtest",
    "code_commit_http_url": "https://bitbucket.org/alauda/buildtest/commits/552819d5c903472a36696e8ac620ac250e49829d",
    "code_repo_branch_url": "https://bitbucket.org/alauda/buildtest/branch/master",
    "is_removable": true
}
```

## 获得某一个构建的详情

`GET /v1/builds/(build_id)`

获得某一个构建的详细信息

**请求示例**:
```
GET /v1/builds/5709f780-e8fb-4b52-aa3b-6256b572fb51
```

**返回示例**:
```json
{
    "build_id": "5709f780-e8fb-4b52-aa3b-6256b572fb51",
    "created_at": "2015-09-02T08:17:42.581Z",
    "started_at": "2015-09-02T08:17:42.691Z",
    "ended_at": "2015-09-02T08:18:13.011Z",
    "code_head_commit": "552819d5c903472a36696e8ac620ac250e49829d",
    "code_repo_client": "Bitbucket",
    "code_repo_path": "alauda/buildtest",
    "code_repo_type": "branch",
    "code_repo_type_value": "master",
    "created_by": "alaudatest",
    "image_id": "a31664dde7e0",
    "docker_repo_path": "alauda/buildtes34t",
    "docker_repo_tag": "latest",
    "docker_repo_version_tag": "v20150902.081742",
    "dockerfile_location": "/",
    "status": "S",
    "auto_created": false,
    "step_at": 50,
    "build_node": "in",
    "build_context_path": "/",
    "code_repo_http_url": "https://bitbucket.org/alauda/buildtest",
    "code_commit_http_url": "https://bitbucket.org/alauda/buildtest/commits/552819d5c903472a36696e8ac620ac250e49829d",
    "code_repo_branch_url": "https://bitbucket.org/alauda/buildtest/branch/master",
    "is_removable": false
}
```

## 获得构建日志

`GET /v1/builds/(build_id)/logs?start_time=(start_time)&end_time=(end_time)`

参数:

- **start_time**(optional) UTC时间的Unix格式，比如1430739601
- **end_time**(optional) UTC时间的Unix格式，比如1430739601

**请求示例**:
```json
GET /v1/builds/a09ec259-eaf8-4345-9692-e8a06ff055ad/logs
```

**返回示例**
```json
[
    {
        "message": "starting to build",
        "level": "INFO",
        "time": 1441770706
    },
    {
        "message": "cloning code source from repo dai92817/test on branch:master",
        "level": "INFO",
        "time": 1441770708
    },
    {
        "message": "Cloning into '/tmp/tmpA5_gNi'...",
        "level": "INFO",
        "time": 1441770709
    },
    {
        "message": "Dockerfile path: /tmp/tmpA5_gNi/Dockerfile. Build context path: /tmp/tmpA5_gNi",
        "level": "INFO",
        "time": 1441770714
    },
    {
        "message": "Sending build context to Docker daemon 3.072 kB",
        "level": "INFO",
    }
    ...
]
```

## 修改构建配置

`PUT /v1/repositories/(namespace)/(repo_name)/build-config`

**请求示例**
```
{
  "build_node": "in",
  "tag_configs": [{
    "id": 1,
    "docker_repo_tag": "release",
    "docker_build_config_id": 1,
    "dockerfile_location": "/",
    "code_repo_type": "branch",
    "code_repo_type_value": "master",
    "is_active": false,
    "version_tagging": 1,
    "build_context_path": "/"
  },
  {
    "docker_repo_tag": "latest",
    "dockerfile_location": "/aa",
    "code_repo_type": "branch",
    "code_repo_type_value": "master",
    "is_active": false,
    "version_tagging": 1,
    "build_context_path": "/aa"
  }]
}
```
