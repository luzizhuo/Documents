## 服务


```
usage: alauda service [-h]

                      {create,run,inspect,start,stop,rm,ps,scale,enable-autoscaling,disable-autoscaling,logs,instances,instance,instance-logs,instance-metrics}
                      ...

Service operations

optional arguments:
  -h, --help            show this help message and exit

Alauda service commands:
  {create,run,inspect,start,stop,rm,ps,scale,enable-autoscaling,disable-autoscaling,logs,instances,instance,instance-logs,instance-metrics}
    create              Create a new service
    run                 Create and start a new service
    inspect             Get details of a service
    start               Start a service
    stop                Stop a service
    rm                  Remove a service
    ps                  List services
    scale               Scale a service
    enable-autoscaling  Enable auto-scaling
    disable-autoscaling Disable auto-scaling
    logs                Query service log
    instances           List instances
    instance            Get details of a instance
    instance-logs       Query instance log
```


示例:

```
bash-3.2# alauda run hello index.alauda.cn/alauda/hello-world:latest -p 80
[alauda] Creating and starting service "hello"
[alauda] OK

```



### create
用于创建一个服务(只创建，不运行)。并通过参数指明服务的名称，所用镜像名称，以及服
务所需容器大小，容器数量等信息。

```
usage: alauda service create [-h] [-t TARGET_NUM_INSTANCES] [-s {XS,S,M,L,XL}]
                             [-r RUN_COMMAND] [-e ENV] [-l LINK] [-p PUBLISH]
                             [-ex EXPOSE] [-v VOLUME] [-n NAMESPACE] [-a]
                             [-f AUTOSCALING_CONFIG] [-d DOMAIN]
                             name image

Create a new service

positional arguments:
  name                  Service name
  image                 Docker image used by the service

optional arguments:
  -h, --help                            show this help message and exit
  -t, --target-num-instances=1          Target number of instances for the service
  -s, --instance-size={XS,S,M,L,XL}     Service container size
  -r, --run-command=""                  The command used to start the service containers
  -e, --env=[]                          Environment variables, e.g. VAR=value
  -l, --link=[]                         which service to link.
  -p, --publish=[]                      Ports to publish, e.g. 5000/tcp
  -ex, --expose=[]                      Internal ports, e.g. 5000
  -v, --volume=[]                       Volumes, e.g. /var/lib/mysql:10
  -n, --namespace=""                    Service namespace
  -a, --autoscale=false                 Enable auto-scaling
  -f, --autoscaling-config=""           Auto-scaling config file name
  -d, --domain=""                       Custom domain name
```


参数:

- 如果显示的指明了`-a` 参数，则表明将服务设置为自动调节模式，此模式下需要使用`-f` 来指明自动调节参数配置文件所在路径。




### run

用于创建并运行一个服务。并通过参数指明服务的名称，所用镜像名称，以及服务所需容器
大小，容器数量等信息。


```
usage: alauda service run [-h] [-t TARGET_NUM_INSTANCES] [-s {XS,S,M,L,XL}]
                          [-r RUN_COMMAND] [-e ENV] [-l LINK] [-p PUBLISH]
                          [-ex EXPOSE] [-v VOLUME] [-n NAMESPACE] [-a]
                          [-f AUTOSCALING_CONFIG] [-d DOMAIN]
                          name image

Create and start a new service

positional arguments:
  name                  Service name
  image                 Docker image used by the service

optional arguments:
  -h, --help                            show this help message and exit
  -t, --target-num-instances=1          Target number of instances for the service
  -s, --instance-size={XS,S,M,L,XL}     Service container size
  -r, --run-command=""                  The command used to start the service containers
  -e, --env=[]                          Environment variables, e.g. VAR=value
  -l, --link=[]                         which service to link.
  -p, --publish=[]                      Ports to publish, e.g. 5000/tcp
  -ex, --expose=[]                      Internal ports, e.g. 5000
  -v, --volume=[]                       Volumes, e.g. /var/lib/mysql:10
  -n, --namespace=""                    Service namespace
  -a, --autoscale=false                 Enable auto-scaling
  -f, --autoscaling-config=""           Auto-scaling config file name
  -d, --domain=""                       Custom domain name
```



### inspect
获取一个服务的详细信息。


```
usage: alauda service inspect [-h] [-n NAMESPACE] name

Get details of a service

positional arguments:
  name                  Name of the service to retrieve

optional arguments:
  -h, --help                show this help message and exit
  -n, --namespace=""        Service namespace
```






### start

启动处于暂停状态的服务。


```
usage: alauda service start [-h] [-n NAMESPACE] name

Start a service

positional arguments:
  name                  Name of the service to start

optional arguments:
  -h, --help                show this help message and exit
  -n, --namespace=""        Service namespace
  ```



### stop
暂停处于运行状态的服务。

```
usage: alauda service stop [-h] [-n NAMESPACE] name

Stop a service

positional arguments:
  name                  Name of the service to stop

optional arguments:
  -h, --help                show this help message and exit
  -n, --namespace=""        Service namespace
```


### rm
删除已存在的服务。


```
usage: alauda service rm [-h] [-n NAMESPACE] name

Remove a service

positional arguments:
  name                  Name of the service to remove

optional arguments:
  -h, --help                show this help message and exit
  -n, --namespace=""        Service namespace
```



### ps
列出当前账户下所有的服务。


```
usage: alauda service ps [-h] [-n NAMESPACE]

List services

optional arguments:
  -h, --help                show this help message and exit
  -n, --namespace=""        Service namespace
```


### scale

调节当前服务中实例数量。



```

usage: alauda service scale [-h] [-n NAMESPACE] [descriptor [descriptor ...]]

Scale a service

positional arguments:
  descriptor            E.g. web=2

optional arguments:
  -h, --help                show this help message and exit
  -n, --namespace=""        Service namespace
```


### enable-autoscaling

将当前服务的状态设置为自动调节模式。

```
usage: alauda service enable-autoscaling [-h] [-n NAMESPACE]
                                         [-f AUTOSCALING_CONFIG]
                                         name

Enable auto-scaling

positional arguments:
  name                  Service name

optional arguments:
  -h, --help                        show this help message and exit
  -n, --namespace=""                Service namespace
  -f, --autoscaling-config=""       Auto-scaling config file name
```


必须显示指明自动调节配置文件所在位置，如果不指明，则默认当前路径下的`auto-scaling.cfg`文件为配置文件。

### disable-autoscaling

将当前服务的状态设置为手动调节模式。


```
usage: alauda service disable-autoscaling [-h] [-n NAMESPACE]
                                          [-t TARGET_NUM_INSTANCES]
                                          name

Disable auto-scaling

positional arguments:
  name                  Service name

optional arguments:
  -h, --help                    show this help message and exit
  -n, --namespace=""            Service namespace
  -t, --target-num-instances=1  Target number of instances for the service
```

设置为手动模式的同时，可以使用`-t`指定服务的实例数量，如果不指定，则以自动调节模式的最后实例数量为当前服务的实例数量。


### logs

查看当前服务的日志信息


```
usage: alauda service logs [-h] [-n NAMESPACE] [-s START_TIME] [-e END_TIME]
                           name

Query service log

positional arguments:
  name                  Service name

optional arguments:
  -h, --help                    show this help message and exit
  -n, --namespace=""            Service namespace
  -s, --start-time=""           Logs query start time. e.g. 2015-05-01 12:12:12
  -e, --end-time=""             Logs query end time. e.g. 2015-05-01 12:12:12
```


如果不指定起始和终止时间，那么返回最近一小时以内的日志。如果只指定起始时间，那么返回指定的起始时间到当前时间的日志，如果只指定终止时间，那么返回终止时间之前一小时以内的日志。



