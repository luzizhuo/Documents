## 获取用户信息

`GET /v1/auth/(namespace)/profile/`

**返回示例** :
```json
{
  "id": 5,
  "last_login": "2015-02-17T07:35:06.253Z",
  "username": "ruicao",
  "email": "ruicao@mathildetech.com",
  "realname": "RuiCao",
  "prefered_language": "zh-cn",
  "is_active": true,
  "is_trialuser": true,
  "password_is_temp": false,
  "joined_at": "2015-02-17T07:35:06.300Z",
  "currency": "CNY",
  "account_type": 1,
  "is_available": true,
  "user_level": "unlimited",
  "company": null,
  "company_website": "",
  "company_size": 0,
  "industry": 0,
  "mobile": null,
  "feature_flags": 65535,
  "logo_file": "https://alauda-cn-jakiro.s3.cn-north-1.amazonaws.com.cn/user/ruicao/logo1434463257.jpg",
  "app_created": "2015-08-04T03:10:49.999Z",
  "repo_created": "2015-07-27T10:34:56.922Z",
  "api_revoked": "2015-08-05T09:09:03.432Z",
  "type": "test"
}
```


参数:
- **namespace** 用户名或机构名
- **currency** 当前账户使用的币种
- **invitation** 邀请码
- **is_available** 账户是否有效
- **password_is_temp** 是否是临时密码
- **is_active** 账户是否已激活
- **user_level** 用户级别（normal表示普通用户，vip表示VIP用户）
- **feature_flags** 用户使用灵雀云的功能标志位
- **app_created** 最后一次操作服务的时间
- **repo_created** 最后一次操作镜像的时间
- **api_revoked** 最后一次使用API的时间
- **type** 用户类型



## 生成 API Token

`POST /v1/generate-api-token/`


**请求示例** :
```json
{
    "username": "madams",
    "password": "a1b2c3d4"
}
```

**返回示例** :
```json
{
    "token": "4dfff64b6d2994a9567ac363149fb8692273e6b2"
}​
```

