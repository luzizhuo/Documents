## 常见错误


### InsecurePlatformWarning

在Centos/Redhat系统，同时python 2.7.9以及以下的版本，在执行任何命令的时候，如果
出现警告：

`InsecurePlatformWarning: A true SSLContext object is not available. This prevents urllib3 from configuring SSL appropriately and may cause certain SSL connections to fail. For more information, see https://urllib3.readthedocs.org/en/latest/security.html#insecureplatformwarning.`


可以尝试:

`pip install pyopenssl ndg-httpsclient pyasn1`


来解决这个问题。如果仍然无法解决这个问题，请登陆我们的系统：https://www.alauda.cn 提交工单，联系我们。
或者在github上提交issue。

