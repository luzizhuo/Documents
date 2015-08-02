## 获取用户信息
`GET /v1/auth/profile/`

**返回示例** :
```json
{
    "id": 23,
    "username": "madams",
    "realname": "michael adams",
    "account_type": 1,
    "currency": "CNY",
    "invitation": "ntev85",
    "is_available": true,
    "is_trialuser": false,
    "password_is_temp": false,
    "email": "michael@yahoo.com",
    "prefered_language": "zh-cn",
    "is_active": true,
    "company": "mathildetech",
    "company_website": "",
    "company_size": 0,
    "industry": 0,
    "last_login": "2015-03-14T05:14:10.031Z",
    "joined_at": "2015-03-14T05:13:55.141Z",
    "user_level": "normal",
    "mobile": "15227452429",
    "feature_flags": 4,
    "logo_file": "/static/images/user/default-logo.png",
    "app_created": "2015-05-14T09:00:36.318Z",
    "repo_created": "2015-05-14T09:01:54.604Z",
    "api_revoked": "2015-05-14T09:49:19.824Z",
    "type": "cn"
}
```


参数:
- **account_type**
- **currency**
- **invitation**
- **is_available**
- **is_trialuser**
- **password_is_temp**
- **is_active**
- **industry**
- **user_level**
- **feature_flags**
- **app_created**
- **repo_created**
- **api_revoked**
- **type**



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

