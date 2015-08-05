## compose

```
usage: alauda compose [-h] {up,ps,start,stop,restart,rm,scale} ...

Compose multi-container app

optional arguments:
  -h, --help            show this help message and exit

Alauda compose commands:
  {up,ps,start,stop,restart,rm,scale}
    up                  Create and start all service containers
    ps                  List containers
    start               Start all service containers
    stop                Stop all service containers
    restart             Restart all service containers
    rm                  Remove all service containers
    scale               Set number of containers to run for a service
```


用于一键部署应用。支持docker-compose的基本命令，并增加了alauda自身的特性。

示例:

```
bash-3.2# alauda compose up -f gitlab.alauda.yml
[alauda] Creating and starting service "postgresql"
[alauda] Creating and starting service "redis"
[alauda] Creating and starting service "gitlab"
[alauda] OK
```



注意:

* volumes的格式修改为path:size path即挂载路径，size为挂载卷大小单位为G。如果不指定size，则默认挂载卷大小为10G。例如:

```yaml
volumes:
- /data:10
- /mnt
```


* ports格式不再支持`port1:port2`，而如下所示:

```yaml
ports:
- "80"
- "22"
或者
ports:
- "80/http"
- "22/tcp"
```

并且ports所映射出的端口是都external性质的。


* expose

expose所暴露出的端口是`internal`性质的。

格式参照参数ports

关于`external`和`internal`的详细说明参照在线文档:[http://docs.alauda.cn/?page_id=123](http://docs.alauda.cn/?page_id=123)



* 在当前的版本中，所有需要暴露的端口，不论external还是internal的都需要显示的在yaml文件中声明，仅仅在Dockerfile中使用EXPOSE命令来声明端口是无效的。


* environment。 支持环境变量的替换。即，某一环境变量可以由当前服务的其他环境变量赋值或者拼接得到。例如:

```yaml
DB_HOST: $POSTGRESQL_PORT_5432_TCP_ADDR
DB_HOST的值就是当前服务中的环境变量POSTGRESQL_PORT_5432_TCP_ADDR所指的值。

```


* 新增size。用于指定服务所需的硬件资源大小。可选范围为{‘XS’, ‘S’, ‘M’, ‘L’,
‘XL’} 例如:

`size: L`

* 新增domain。 用于用户指定自己的域名。例如:

`domain: "www.myself.com"`

* 新增autoscaling_config。用于指定服务的自动调节模式，以及自动调节模式的配置文件。
例如:

`autoscaling_config: ./autoscaling.cfg`

* 新增number。用户指定某个服务所开启的实例数量。例如:
`size: 5`


### up

启动包含多个服务的应用。

```
usage: alauda compose up [-h] [-f FILE] [-s]

Create and start all service containers

optional arguments:
  -h, --help            show this help message and exit
  -f, --file=""         Compose file name
  -s, --strict=false    Wait for linked services to start
```


当显示的输入-s 参数时，表示服务需要等到其所link的服务启动之后，才开始启动。


### ps
列出应用的各个服务信息。

```
usage: alauda compose ps [-h] [-f FILE]

Lists container

optional arguments:
  -h, --help            show this help message and exit
  -f, --file=""         Compose file name
```


### start

启动已经停止的应用。

```
usage: alauda compose start [-h] [-f FILE] [-s]

Start all service containers

optional arguments:
  -h, --help            show this help message and exit
  -f, --file=""         Compose file name
  -s, --strict          Wait for linked services to start
```


`-s` 同 `up`命令


### stop

暂停运行中的应用。


```
usage: alauda compose stop [-h] [-f FILE]

Stop all service containers

optional arguments:
  -h, --help            show this help message and exit
  -f, --file=""         Compose file name
```


### restart

重新启动应用。

```
usage: alauda compose restart [-h] [-f FILE] [-s]

Restart all service containers

optional arguments:
  -h, --help            show this help message and exit
  -f, --file=""         Compose file name
  -s, --strict          Wait for linked services to start
```


### rm
删除应用。

```
sage: alauda compose rm [-h] [-f FILE]

Remove all service containers

optional arguments:
  -h, --help            show this help message and exit
  -f, --file=""         Compose file name
```


### scale

调节应用中每个服务的实例数量。


```
usage: alauda compose scale [-h] [-f FILE] [descriptor [descriptor ...]]

Set number of containers to run for a service

positional arguments:
  descriptor            E.g. web=2 db=1

optional arguments:
  -h, --help            show this help message and exit
  -f, --file=""         Compose file name
```


示例:

`alauda compose scale web=2 redis=3`






