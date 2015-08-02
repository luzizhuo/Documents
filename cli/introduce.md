## Alauda Command Line

## 源码
开源地址:

`https://github.com/alaudacloud/alauda-CLI.git`


## 安装

`pip install alauda`


## 使用
`alauda` 或 `alauda -h`:

```bash
bash-3.2# alauda
usage: alauda [-h] [-v] {login,logout,service,compose,backup,organization} ...

Alauda CLI

optional arguments:
  -h, --help            show this help message and exit
  -v, --version         show program's version number and exit

Alauda CLI commands:
  {login,logout,service,compose,backup,organization}
    login               Alauda login
    logout              Log out
    service             Service operations
    compose             Compose multi-container app
    backup              Backup operations
    organization        Organization operations
```


使用 `-v` 来查看当前 alauda CLI的版本:

```bash
bash-3.2# alauda -v
alauda 0.1.0
```

在后面所有的参数说明中:

* `-e[]` 表示可以志明多次
  比如`-e DB_NAME=mysql -e DB_PASSOWRD=123`
* `-d=""` 表示值是字符串
  例如`-d "www.myself-domain.com"`
* `-s=[XS,S,M,L,XL]` 表示必须是给定的值之一
  例如: `-s XL`
* `-t=1` 表示所给定的值必须为数字
  例如: `-t 1`
* `-a=false` 表示不显示输出此参数的情况下，参数的值为false即无效状态，如果显示的列出该参数 `-a`，则表明该参数的值为true，即有效状态。



## 帮助
显示任何支持命令的帮助信息，只需要在命令后面增加参数`-h`


```bash
bash-3.2# alauda service create -h
usage: alauda service create [-h] [-t TARGET_NUM_INSTANCES] [-s {XS,S,M,L,XL}]
                             [-r RUN_COMMAND] [-e ENV] [-l LINK] [-p PUBLISH]
                             [-v VOLUME] [-n NAMESPACE] [-a]
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



