
**default:** *"TWAF_mcrawler"*

**context:** *twaf_anti_mail_crawler*

被识别为恶意爬虫时，发送cookie的名称，默认"TWAF_crawler"

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

###action_meta
**syntax:** *"action_meta": number|string*

**default:** *403*

**context:** *twaf_anti_mail_crawler*

动作附属信息

若动作为"DENY"时，action_meta表示响应码  
若动作为"REDIRECT"时，action_meta表示重定向路径  

