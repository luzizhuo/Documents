## 命令补全


支持命令补全和查找。例如在输入alauda之后，双击Tab键，即可看到alauda支持的命令。
在键入alauda compse之后双击Tab键，就可以知道alauda compose 所支持的命令。 当输出
alauda c之后，单机Tab键，即可得到补全后的命令alauda compose



###  Debian

只需要将源码包中的alauda文件拷贝到/etc/bash_completion.d，然后执行


`. /etc/bash_completion.d/alauda`


### OS X

首先需要安装 bash-completion

```
$ brew install bash-completion
$ brew tap homebrew/completions
```


然后将源码包中的alauda文件拷贝到/usr/local/etc/bash_completion.d/,然后执行

`. /usr/local/etc/bash_completion.d/alauda`

即可.



