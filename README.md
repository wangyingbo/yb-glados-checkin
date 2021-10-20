# yb-glados-checkin


## 用于腾讯云函数的glados签到脚本

**使用说明**

### 一、部署腾讯云函数，拷贝本仓库的`checkin.py`脚本

### 二、各个字段解释如下：

- sever：server酱开关，`on`是打开状态；`off`失败状态；
- sckey：server酱的key，如果不需要推送，留空即可；申请地址见：[申请server酱key](https://sct.ftqq.com/sendkey) ，申请非常简单，微信扫码登录后即可直接获取key；

### 三、修改自己glados的账户的cookie
-  key是在有多个账号情况下，用server酱推送到手机时，区分是哪个账号用的，建议key是邮箱名

```
    dict['key1'] = "first_cookie"
    dict['key2'] = "second_cookie"
    dict['key3'] = "third_cookie"
    
```
