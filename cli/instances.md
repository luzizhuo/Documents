## 实例


### instance

查看某一个实例的详细信息。


```
Get details of a instance

positional arguments:
  name                  Service name
  id                    Instance uuid

optional arguments:
  -h, --help                show this help message and exit
  -n, --namespace=""        Service namespace
```





### instance-logs

查看某一实例的日志信息。



```
usage: alauda service instance-logs [-h] [-s START_TIME] [-e END_TIME]
                                    [-n NAMESPACE]
                                    name id

Query instance log

positional arguments:
  name                  Service name
  id                    Instance uuid

optional arguments:
  -h, --help                    show this help message and exit
  -s, --start-time=""           Logs query start time. e.g. 2015-05-01 12:12:12
  -e, --end-time=""             Logs query end time. e.g. 2015-05-01 12:12:12
  -n, --namespace=""            Service namespace
```
