# yb-glados-checkin


## 用于腾讯云函数的glados签到脚本；[云函数地址](https://console.cloud.tencent.com/scf/index?rid=15)

**使用说明**

### 一、部署腾讯云函数，拷贝本仓库的`glados_checkin.py`脚本

### 二、各个字段解释如下：

- sever：server酱开关，`on`是打开状态；`off`关闭状态；
- sckey：server酱的key，如果不需要推送，留空即可；申请地址见：[申请server酱key](https://sct.ftqq.com/sendkey) ，申请key微信扫码登录后即可直接获取key；

### 三、修改自己glados的账户的cookie
-  key是在有多个账号情况下，用server酱推送到手机时，区分是哪个账号用的，建议key是邮箱名

```
    dict['key1'] = "first_cookie"
    dict['key2'] = "second_cookie"
    dict['key3'] = "third_cookie"
    
```

### 四、配置云函数的触发定时任务，参照[crontab](https://crontab.guru/)表达式；

### 五、仓库中`per_glados_checkin.py`脚本是通过一个脚本给多个用户签到的脚本，可支持server酱推送和企业微信推送下两种：

- 如果是通过server酱推送签到成功通知，则dict的key为"邮箱&&sckey"，dict的value为本用户的cookie；如果只想签到而不想推送，则sckey用`none`代替；

```
	dict = {}
	# 以&&分割，前面的是邮箱，后面是推送到微信的server酱的sckey
	dict['qq_mail&&sckey'] = "first_user_cookie"
```

- 如果是通过企业微信推送给微信来推送签到成功通知，则dictWC的key为"邮箱&&user"，user可用"|"分割拼接多个；dictWC的value为本用户的cookie；如果只想签到而不想推送，则user用`none`代替；

```
	dictWC = {}
	# 以&&分割，前面的是邮箱，后面是利用企业微信推送到微信的user，user可用"|"分割拼接多个；
	dictWC['qq_mail&&user'] = "first_user_cookie"
```

- 可以通过创建对象来创建每个用户，第一个参数为名字，第二个参数为server酱的key，第三个参数为企业微信的user，第四个为cookie；

```
    # 第一个用户
    user1 = Model("2532084725_qq","none","wangyingbo","first_user_cookie")
    objArray.append(user1)

    # 第二个用户
    user2 = Model("wangyingbo0528_gmail","none","wangyingbo","second_user_cookie")
    objArray.append(user2)
```