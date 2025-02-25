# 智能号码认证产品API文档

- - - - -

***版权所有 翻版必究***

- - - - -

* [一键登录接口](#oneClickleInterface)
    + [请求参数](#requestParameter)
        - [请求URL](#requestUrl)
        - [字符编码格式](#requestEncode)
        - [请求方法](#requestMethod)
        - [建议超时时长](#requestTimeout)
        - [请求参数](#requestParameters)
    + [返回结果](#response)
    + [示例](#example)
        - [请求示例](#requestExample)
        - [返回示例](#responseExample)
* [本机号码验证接口](#phoneVerifyleInterface)
    + [请求参数](#requestParameter)
        - [请求URL](#requestUrl)
        - [字符编码格式](#requestEncode)
        - [请求方法](#requestMethod)
        - [建议超时时长](#requestTimeout)
        - [请求参数](#requestParameters)
    + [返回结果](#response)
    + [示例](#example)
        - [请求示例](#requestExample)
        - [返回示例](#responseExample)

# <span id = "oneClickleInterface">一键登录接口</span>

## <span id = "requestParameter">一键登录请求</span>

### <span id = "requestUrl">请求URL：</span>
| 集群 | URL | 支持产品列表 |
| --- | --- | --- |
| 北京 | `http://api-oneclick-bj.fengkongcloud.com/oneclick/v1` | 一键登录 |

### <span id = "requestMethod">请求方法：</span>

`POST` 

### <span id = "requestEncode">字符编码：</span>

`UTF-8`

### <span id = "requestTimeout">建议超时时间：</span>

2s

### <span id = "requestParameters">请求参数：</span>

放在HTTP Body中，采用Json格式，具体参数如下：
| **请求参数名** | **类型** | **参数说明** | **传入说明** | **规范** |
| --- | --- | --- | --- | --- |
| accessKey | string | 接口认证密钥<br/>用于权限认证，开通账号服务时由数美提供或使用开通邮箱登录数美后台右上角相关文档处查看 | 必传参数 | accessKey |
| appId | string | 应用标识，用于区分相同公司的不同应用数据 | 必传参数 | 默认应用值：`default`<br/>传递其他值时需联系数美服务协助开通 |
| data | json_object | 请求的数据内容 | 必传参数 | 请求的数据内容，最长10MB，[详见data参数](#data) |

<span id = "data">其中，data的内容如下：</span>

| **请求参数名** | **类型** | **参数说明** | **是否必传** | **规范** |
| --- | --- | --- | --- | --- |
| tokenId | string | 用户账号标识，建议使用贵司用户UID（可加密）自行生成 , 标识用户唯一身份用作灌水和广告等行为维度风控。如无用户uid的场景建议使用唯一的数据标识传值 | 非必传参数 | 由数字、字母、下划线、短杠组成的长度小于等于64位的字符串 |
| accessToken | string | 运营商授权码，用于向运营商获取手机号 | 必传参数 | 调用数美sdk获取 |
| os | string | 平台类型标识 | 必传参数 | 平台类型<br/>可选值：<br/>`andrid`<br/>`ios`<br/>`weapp`<br/>`h5` |
| deviceInfo  | string | 加密的浏览器指纹，由weapp/h5端SDK采集。android/ios可传空值 | 必传参数 | 调用数美sdk获取 |

## <span id = "response">返回结果</span>

放在HTTP Body中，采用Json格式，具体参数如下：

| **参数名称** | **参数类型** | **参数说明** | **是否必返** | **规范** |
| --- | --- | --- | --- | --- |
| code | int | 返回码 | 是 |  `1100`：成功<br/>`1901`：QPS超限<br/>`1902`：参数不合法<br/>`1903`：服务失败<br/>`1911`：图片下载失败<br/>`9101`：无权限操作<br/>`3000`：运营商错误<br/>除message和requestId之外的字段，只有当code为1100时才会存在 |
| message | string | 返回码描述 | 是 | 和code对应：成功QPS超限参数不合法服务失败余额不足无权限操作 |
| requestId | string | 请求标识 | 是 | 请求唯一标识，用于排查问题和后续效果优化，强烈建议保存 |
| phoneRsa | string | 请求结果 | 是 | 加密后的手机号，加密方式为：RSA加密，客户使用私钥解密 |

## <span id = "example">示例：</span>

### <span id = "requestExample">请求示例：</span>

```json
{
    "accessKey":"",
    "appId":"",
    "data":{
        "tokenId":"username123",
        "accessToken":"",
        "os":"android",
        "deviceInfo":""
    }
}
```

### <span id = "syncResponseExample">同步返回示例：</span>

```json
{
    "code":1100,
    "message":"成功",
    "requestId":"69dbc1f81dc5c914b1f1b8a267fb9ec1",
    "phoneRsa":""
}
```

# <span id = "phoneVerifyleInterface">本机号码校验接口</span>

## <span id = "requestParameter">本机号码校验请求</span>

### <span id = "requestUrl">请求URL：</span>
| 集群 | URL | 支持产品列表 |
| --- | --- | --- |
| 北京 | `http://api-phoneverify-bj.fengkongcloud.com/phoneverify/v1` | 本机号码校验 |

### <span id = "requestMethod">请求方法：</span>

`POST` 

### <span id = "requestEncode">字符编码：</span>

`UTF-8`

### <span id = "requestTimeout">建议超时时间：</span>

2s

### <span id = "requestParameters">请求参数：</span>

放在HTTP Body中，采用Json格式，具体参数如下：
| **请求参数名** | **类型** | **参数说明** | **传入说明** | **规范** |
| --- | --- | --- | --- | --- |
| accessKey | string | 接口认证密钥<br/>用于权限认证，开通账号服务时由数美提供或使用开通邮箱登录数美后台右上角相关文档处查看 | 必传参数 | accessKey |
| appId | string | 应用标识，用于区分相同公司的不同应用数据 | 必传参数 | 默认应用值：`default`<br/>传递其他值时需联系数美服务协助开通 |
| eventId | string | 时间标识 | 必传参数 | 在本机号码验证场景中建议传入进行区分，否则为`default` |
| data | json_object | 请求的数据内容 | 必传参数 | 请求的数据内容，最长10MB，[详见data参数](#data) |

<span id = "data">其中，data的内容如下：</span>

| **请求参数名** | **类型** | **参数说明** | **是否必传** | **规范** |
| --- | --- | --- | --- | --- |
| lastReq | string | 前置天网事件请求标识 | 非必传参数 | 前置天网事件返回的请求requestId |
| tokenId | string | 用户账号标识，建议使用贵司用户UID（可加密）自行生成 , 标识用户唯一身份用作灌水和广告等行为维度风控。如无用户uid的场景建议使用唯一的数据标识传值 | 非必传参数 | 由数字、字母、下划线、短杠组成的长度小于等于64位的字符串 |
| accessToken | string | 运营商授权码，用于向运营商获取手机号 | 必传参数 | 调用数美sdk获取 |
| phoneRsa | string | 手机号 | 必传参数 | 加密后的手机号，用于后续向运营商进行认证是否为本机号码<br/>加密方式：RSA加密。请求时使用公钥加密 |
| os | string | 平台类型标识 | 必传参数 | 平台类型<br/>可选值：<br/>`andrid`<br/>`ios`<br/>`weapp`<br/>`h5` |
| deviceInfo  | string | 加密的浏览器指纹，由weapp/h5端SDK采集。android/ios可传空值 | 必传参数 | 调用数美sdk获取 |

## <span id = "response">返回结果</span>

放在HTTP Body中，采用Json格式，具体参数如下：

| **参数名称** | **参数类型** | **参数说明** | **是否必返** | **规范** |
| --- | --- | --- | --- | --- |
| code | int | 返回码 | 是 |  `1100`：成功<br/>`1901`：QPS超限<br/>`1902`：参数不合法<br/>`1903`：服务失败<br/>`1911`：图片下载失败<br/>`9101`：无权限操作<br/>`3000`：运营商错误<br/>除message和requestId之外的字段，只有当code为1100时才会存在 |
| message | string | 返回码描述 | 是 | 和code对应：成功QPS超限参数不合法服务失败余额不足无权限操作 |
| requestId | string | 请求标识 | 是 | 请求唯一标识，用于排查问题和后续效果优化，强烈建议保存 |
| riskLevel | string | 验证结果 | 是 | 可能返回值：<br/>`PASS`：正常（运营商返回认证通过）<br/>`REVIEW`：重试（运营商返回无法确认）<br/>`REJECT`：拒绝（运营商返回认证不通过） |

## <span id = "example">示例：</span>

### <span id = "requestExample">请求示例：</span>

```json
{
    "accessKey":"",
    "appId":"",
    "eventId":"",
    "data":{
        "lastReq":"",
        "tokenId":"username123",
        "accessToken":"",
        "phoneRsa":"",
        "os":"android",
        "deviceInfo":""
    }
```

### <span id = "syncResponseExample">同步返回示例：</span>

```json
{
    "code":1100,
    "message":"成功",
    "requestId":"69dbc1f81dc5c914b1f1b8a267fb9ec1",
    "verifyResult":3
}
```