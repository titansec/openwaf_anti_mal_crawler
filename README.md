Nmae
====

openwaf_anti_mail_crawler是[openwaf](https://github.com/titansec/openwaf)的子模块，用于防恶意爬虫，防部分恶意扫描

Configuration Directives
========================

```txt
        "state": false,                              -- 模块开关
        "log_state":true,                            -- 日志开关

        "shared_dict_name":"twaf_shm",               -- shared_dict名称
        "shared_dict_key": "remote_addr",            -- shared_dict键值
        "timeout":300,                               -- shared_dict保存状态有效时长（单位秒）
        "timer_flush_expired":200,                   -- shared_dict清除过期信息的间隔时间（单位秒）,若为空，则值为"twaf_global"下的"timer_flush_expired"

        "cookie_state":true,                         -- cookie机制开关
        "crawler_cookie_name":"TWAF_crawler",        -- 爬虫cookie名称
        "mal_cookie_name":"TWAF_mcrawler",           -- 恶意爬虫cookie名称

        "force_scan_robots_state":true,              -- 页面注入诱捕路径的开关
        "force_scan_times": 3,                       -- 注入诱捕路径的页面个数
        "trap_uri":"/abc/abc.html",                  -- 诱捕路径
        "trap_args":"id=1",                          -- 诱捕参数

        "action":"ALLOW",                            -- 执行动作，支持"ALLOW", "DENY","REDIRECT", "ROBOT", "RESET_CONNECTION","PASS"
        "action_meta": 403                           -- 执行动作的附属信息，若action为DENY，action_meta为响应码，若action为REDIRECT，action_meta为重定向url
```

###state
**syntax:** *"state": true|false*

**default:** *true*

**context:** *twaf_anti_mail_crawler*

模块开关，支持true和false，默认false

###log_state
**syntax:** *"log_state": true|false*

**default:** *true*

**context:** *twaf_anti_mail_crawler*

模块日志开关，支持true和false，默认true

###shared_dict_name
**syntax:** *"shared_dict_name": string*

**default:** *"twaf_shm"*

**context:** *twaf_anti_mail_crawler*

共享内存名称，默认为twaf_global中共享内存的名称("twaf_shm")

###shared_dict_key
**syntax:** *"shared_dict_key": var | var array*

**default:** *"remote_addr"*

**context:** *twaf_anti_mail_crawler*

共享内存键值，支持变量字符串或变量数组，默认为客户端地址"remote_addr"(忽略大小写)

变量字符串
```json
    "shared_dict_key": "remote_addr"
```

变量数组
```json
    "shared_dict_key": ["remote_addr", "user-agent"]
```

###timeout
**syntax:** *"timeout": number*

**default:** *300*

**context:** *twaf_anti_mail_crawler*

拦截有效时长，默认300秒，

被认定为恶意爬虫，300秒内访问，时间重置，且拦截请求

###timer_flush_expired
**syntax:** *"timer_flush_expired": number*

**default:** *200*

**context:** *twaf_anti_mail_crawler*

shared_dict清除过期信息的间隔时间（单位秒）

###cookie_state
**syntax:** *"cookie_state": true|false*

**default:** *true*

**context:** *twaf_anti_mail_crawler*

cookie机制开关，支持true和false，默认true

###crawler_cookie_name
**syntax:** *"crawler_cookie_name": TWAF_xxxx*

**default:** *"TWAF_crawler"*

**context:** *twaf_anti_mail_crawler*

被识别为爬虫时，发送cookie的名称，默认"TWAF_crawler"

注意：  
1. 此指令只有在cookie_state开启时生效  
2. 若开启cookie防篡改模块（openwaf_cookie_guard暂未开源），必须以"TWAF_"开头  

###mal_cookie_name
**syntax:** *"mal_cookie_name": TWAF_xxxx*

**default:** *"TWAF_mcrawler"*

**context:** *twaf_anti_mail_crawler*

被识别为恶意爬虫时，发送cookie的名称，默认"TWAF_mcrawler"

注意：  
1. 此指令只有在cookie_state开启时生效  
2. 若开启cookie防篡改模块（openwaf_cookie_guard暂未开源），必须以"TWAF_"开头  

###force_scan_robots_state
**syntax:** *"force_scan_robots_state": true|false*

**default:** *true*

**context:** *twaf_anti_mail_crawler*

页面注入诱捕路径（暗链）的开关，支持true和false，默认true

###force_scan_times
**syntax:** *"force_scan_times": number**

**default:** *3*

**context:** *twaf_anti_mail_crawler*

注入诱捕路径的页面个数，默认3个

###trap_uri
**syntax:** *"trap_uri": uri*

**default:** *"/abc/abc.html"*

**context:** *twaf_anti_mail_crawler*

设置诱捕路径，默认为"/abc/abc.html"

###trap_args
**syntax:** *"trap_args": args*

**default:** *"id=1"*

**context:** *twaf_anti_mail_crawler*

设置诱捕参数

访问诱捕路劲，被认定为恶意爬虫  
若未被认定为恶意爬虫时，携带设置的参数，访问诱捕路径，不会被认定为恶意爬虫  

###action
**syntax:** *"action": string*

**default:** *"DENY"*

**context:** *twaf_anti_mail_crawler*

被认定为恶意爬虫时执行的动作，默认拦截"DNEY"  
动作支持拦截("DENY"),重定向("REDIRECT"),连接重置("RESET_CONNECTION")，放行("PASS")
###action_meta
**syntax:** *"action_meta": number|string*

**default:** *403*

**context:** *twaf_anti_mail_crawler*

动作附属信息

若动作为"DENY"时，action_meta表示响应码  
若动作为"REDIRECT"时，action_meta表示重定向路径  

