#Alauda Web钩子

Alauda用户可以为镜像仓库创建Web钩子以监听某些特定事件比如构建完成、镜像推送等。当这些事件发生时，钩子会向指定的URL发送HTTP POST请求。用户的程序收到请求后，可以根据自己的需求来执行任务，比如自动部署、自动化测试等。请注意，钩子的请求方式是POST，发送的数据格式是JSON，超时为30秒。

##Alauda事件

目前，Alauda支持的事件如下：

- **build:complete** 当镜像构建仓库的构建完成时触发该事件

- **image:push** 当镜像被推送到镜像仓库时触发该事件

##Web钩子请求

当某事件发生时，钩子会发送请求。请注意，不同事件触发的请求，发送的数据格式是不同的。

####请求头部

- **User-Agent** 请求的用户代理是Alauda/Webhook/1.0
- **X-Alauda-Event** 事件名称，比如build:complete
- **X-Alauda-Event-Time** 事件发生的UTC时间，比如2015-08-27T06:08:55.092827Z
- **X-Alauda-Signature** 事件发生时间的HAMC-SHA1签名，该签名基于Web钩子里设置的密钥，比如
sha1=201d80bab93c9e6b790e3c3ed53a7f604a1cc5c9

####请求内容示例（build:complete）
```json
{
    'hook': {
        'id': 1,
        'subject_type': 'build_repo',
        'subject': ‘alaudauser/build_repo_demo'
    },
    'data': {
        'build_id': '85d61cb5-8827-46a2-9c38-40ce72d3f704',
        'docker_repo_path': 'alaudauser/build_repo_demo',
        'created_by': 'alaudauser',
        'code_repo_type_value': 'master',
        'docker_repo_version_tag': 'v20150827.060840',
        'status': 'F',
       …
       …
    },
    'sender': {
        'username': 'alaudauser'
    }
}
```

####计算签名的代码示例（python）

	import hashlib
	import hmac

	signature = hmac.new(hook_secret, '2015-08-27T06:08:55.092827Z', hashlib.sha1).hexdigest()

##创建web钩子

1. 访问镜像（构建）仓库页面，点击链接“Web钩子”

2. 点击创建Web钩子

3. 填入必须的字段，点击“创建”。基于安全性考虑，密钥用来计算对事件发生时间做的的数字签名，用户可以核对该请求是否来自Alauda。

4. 创建成功后，页面会跳到Web钩子列表

