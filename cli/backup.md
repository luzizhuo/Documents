### backup

```bash
usage: alauda backup [-h] {create,list,inspect,rm} ...

Backup operations

optional arguments:
  -h, --help            show this help message and exit

Alauda backup commands:
  {create,list,inspect,rm}
    create              Create a new volume backup
    list                List volume backups
    inspect             Get details of a volume backup
    rm                  Remove a volume backup
```


用于对服务的数据进行备份。这些数据必须是存储在卷中。


示例:

```bash
bash-3.2# alauda backup create backup1 redis /data
[alauda] Creating backup "backup1"
[alauda] OK
```

### create

创建备份。


```bash
usage: alauda backup create [-h] [-n NAMESPACE] name service dir

Create a new volume backup

positional arguments:
  name                  Backup name
  service               Name of the service to create volume backup for
  dir                   Mounted volume directory to backup

optional arguments:
  -h, --help            show this help message and exit
  -n, --namespace=""    Service namespace
```


参数dir 是服务在创建的时候所制定的volume挂载路径。


### list

列出当前所有备份。

```bash
usage: alauda backup list [-h] [-n NAMESPACE]

list volume backups

optional arguments:
  -h, --help            show this help message and exit
  -n, --namespace=""    Service namespace
```


### inspect

获取某个备份的详细信息。


```bash
usage: alauda backup inspect [-h] [-n NAMESPACE] id

Get details of a volume backup

positional arguments:
  id                    UUID of the volume backup

optional arguments:
  -h, --help            show this help message and exit
  -n, --namespace=""    Service namespace
```


id 为用户创建每个备份之后所获取的唯一id。





### rm

删除备份。

```bash
usage: alauda backup rm [-h] [-n NAMESPACE] id

Remove a volume backup

positional arguments:
  id                    UUID of the volume backup

optional arguments:
  -h, --help            show this help message and exit
  -n, --namespace=""    Service namespace
```





