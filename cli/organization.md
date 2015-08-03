## organization

```bash
usage: alauda organization [-h] {list,create,inspect,update} ...

Organization operations

optional arguments:
  -h, --help            show this help message and exit

Alauda organization commands:
  {list,create,inspect,update}
    list                List all organization
    create              Create a new organization
    inspect             Get details of an organization
    update              Update an exist orgnization

```


在当前账户下创建机构，并进行管理。这些机构和普通账户一样，可以进行服务的构建等操作。管理员可以增减机构中的用户数量，或者对机构中的某一用户的权限进行修改。有只读、可写、管理员权限等。

样例:

```bash
bash-3.2# alauda organization list
     Name           Company              Created time
-----------------------------------------------------------
mathildedev      云雀科技研发组        2015-04-25T05:42:00.828Z
xdzhangcnorg     mathilde          2015-05-19T03:35:29.047Z
xdzhangcnorg1    mathilde2         2015-05-25T07:38:07.670Z

```



### create
创建组织。

```bash
usage: alauda organization create [-h] name company

Create a new organization

positional arguments:
  name        Organization name
  company     Company name

optional arguments:
  -h, --help  show this help message and exit
  ```


### list

列出当前用户所属的所有组织。


### inspect

获取某个组织的详细信息。


```bash
usage: alauda organization inspect [-h] name

Get details of an organization

positional arguments:
  name        Organization name

optional arguments:
  -h, --help  show this help message and exit
```

### update

更新某个组织的信息



```bash
usage: alauda organization update [-h] name company

Update an exist orgnization

positional arguments:
  name        Organization name
  company     Company name

optional arguments:
  -h, --help  show this help message and exit
```


