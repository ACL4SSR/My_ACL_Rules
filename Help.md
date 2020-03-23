# 1. 前言

​	本文主要是教你怎么定制一下自己的ACL或者clash规则。

​	前面稍微科普一下去广告的分类、不作为重点。

​	本文不能顾及全网的规则，仅做一般普及，需要有点基础，非小白科普文章
​	
	**版权所有，所有内容全部一个个字码出来的，转载必须说明来源**

​	**ACL4SSR在线Clash等规则订阅转换**：https://acl4ssr.netlify.com

​	**项目镜像**：https://cdn.jsdelivr.net/gh/ACL4SSR/ACL4SSR@latest/

​	**项目地址**：https://github.com/ACL4SSR/ACL4SSR



## 1.0 去广告的种类

### 域名屏蔽类型

​	核心思路是让带有广告内容的域名，直接屏蔽，不让访问。

​	主要有去广告hosts、去广告的DNS、SSR的ACL、PAC、Clash和Surge等方式。

​	**优点：** 效率高、速度快、对设备支持度非常广

​	**缺点：**  屏蔽效率不高，遇见广告内容和正常内容共用一个域名的没辙



### 网址屏蔽类型

​	核心思路是解析访问网址，将是广告网址进行屏蔽。网址屏蔽一般也包含域名屏蔽。

​	只要有ABP、AdGuard 。

​	**优点：** 屏蔽力度细、可以较好的区分同一域名的广告链接和正常链接，防止误屏蔽

​	**缺点：** 效率一般，对HTTP请求过滤比较好，HTTPS则需要配合中间人攻击(MITM)解密流量才能进行破解



### 页面样式屏蔽

​	核心思路是我屏蔽不了你的广告网络请求，但是我能屏蔽你，不让你露出，眼不见为净

​	可以屏蔽页面元素、修改请求的HTML内容

​	有ABP、浏览器去广告插件、各种修改去广告的APP

​	**优点：** 屏蔽力度非常细、防止误屏蔽

​	**缺点：** 需要软件支持，入侵比较大



## 1.2 客户端

hosts：域名屏蔽

DNS：域名屏蔽

SSR的ACL：域名屏蔽

PAC：域名屏蔽类型

Clash规则：域名屏蔽

Surge：域名屏蔽类型+网址屏蔽

ABP：域名屏蔽类型+网址屏蔽+页面样式

AdGuard ：域名屏蔽类型+网址屏蔽+页面样式



# 2. 规则分类

​	定制规则，其实就将流量合理的分配一下，该代理的代理、该直连的直连、改屏蔽的屏蔽。

​	规则追求的是精简高效。



## 2.0 市面上常见碎片集

**ACL4SSR**

​	https://github.com/ACL4SSR/ACL4SSR/tree/master/Clash

​	subconverter\rules\ACL4SSR\Clash

**lhie1**

​	https://github.com/lhie1/Rules/blob/master/Surge/Surge%203/Provider/

**ConnersHua**

​	https://github.com/ConnersHua/Profiles/tree/master/Surge/Ruleset

​	subconverter\rules\ConnersHua\Surge\Ruleset



## 2.2 去广告

### ACL4SSR去广告碎片

**介绍：**将去广告分的比较细，每一块都有说明，定制化比较强。	

| 文件                  | 类型     | 解释                                                         |
| --------------------- | :------- | ------------------------------------------------------------ |
| BanAD.list            | 广告联盟 | 只包含常见广告关键字、广告联盟。无副作用，放心使用           |
| BanProgramAD.list     | 应用广告 | 常用应用的去广告，比如网站、视频等<br/>可能有轻微副作用，可放心使用。<br/>（如果网站功能和广告冲突，会删掉去广告规则） |
| BanEasyListChina.list | 广告扩展 | AdblockPlus中的中国所有的屏蔽域名                            |



### lhie1去广告碎片

**介绍：**

​	将各种去广告都放在一起了。

​	除了视频是分块有介绍的，剩下的都合并到一个列表里了。

| 文件        | 类型 | 解释                             |
| ----------- | :--- | -------------------------------- |
| Reject.list |      | 视频广告、网站广告、垃圾网站广告 |



### ConnersHua去广告碎片

**介绍：**

​	分门别类，注释的还是很清除的

​	运营商劫持是亮点

| 文件             | 类型 | 解释                   |
| ---------------- | :--- | ---------------------- |
| Advertising.list |      | 少量广告联盟、应用广告 |
| Hijacking.list   |      | 运营商劫持、恶意网站   |



### 使用建议

​	3家去广告总体来说差不多，选择一家足够。日常使用区别不大

​	一般来说选择其中一家的足够，觉得不够的话，最多合并2家。

​	但是非常不推荐全部加上，因为重复度过高，误拦也比较严重



**轻度使用：**

​	会有一些广告拦截不了，但是不会影响正常使用

电脑上使用

​	BanAD.list+BanProgramAD.list+浏览器ABP去广告扩展

手机、路由

​	BanAD.list+BanProgramAD.list+BanEasyListChina.list



**中度使用：**

​	方案1：BanAD.list+BanProgramAD.list+BanEasyListChina.list+Hijacking.list

​	方案2：Reject.list + Hijacking.list

​	方案3：Advertising.list + Hijacking.list



**重度使用：**

​	方案1：BanAD.list+BanProgramAD.list+BanEasyListChina.list+Advertising.list + Hijacking.list

​	方案2：Reject.list+Advertising.list + Hijacking.list



**极限玩家：**

​	全都加上



**去广告DNS**


​	https://www.onedns.net/personal

​	**117.50.11.11 52.80.66.66**



## 2.3 直连

​	主要分为这几类：本地/局域网地址、中国本地IP和域名、国外能直连的IP和域名

### ACL4SSR的直连碎片

说明

​	分的很细，直连域名能比别家全一些，

​	亮点1：ChinaCompanyIp.list。一般在BAT云服务器上的网站都会直连，比如香港的

​	亮点2：GoogleCN.list。谷歌在中国能直连的域名，可以修复一些谷歌服务不正常。

| 文件                  | 类型          | 解释                                                         |
| --------------------- | ------------- | ------------------------------------------------------------ |
| LocalAreaNetwork.list | 规则碎片-直连 | 本地地址和路由器直连域名啥的                                 |
| ChinaDomain.list      | 规则碎片-直连 | 国内常见域名、直连CDN等。（很全，常用网址都有）              |
| ChinaCompanyIp.list   | 规则碎片-直连 | 国内BAT公司及云服务厂商的IP段。所有在该云服务上的网站都可以直连。比如你网站在阿里云香港都可以直连。 |
| ChinaIp.list          | 规则碎片-直连 | IPIP的国内地址段，比GeoIp准确度高很多。<br/>但因为是按条排列，查找效率很低<br/>不推荐使用，电脑性能好，可以引入 |
| Download.list         | 规则碎片-直连 | 一些下载用的域名                                             |
| GoogleCN.list         | 规则碎片-直连 | 谷歌在中国能直连的网址列表                                   |



### lhie1直连碎片

**介绍：**

​	比较全。

​	亮点是有特殊直连域名 需要放拦截列表前面

| 文件          | 类型 | 解释                                            |
| ------------- | :--- | ----------------------------------------------- |
| Domestic.list | 直连 | 常见直连域名                                    |
| AsianTV.list  | 直连 | 中国几个常见的视频网址                          |
| Special.list  | 直连 | 需要特殊放行的几个域名<br/>一般放在拦截列表前面 |



### ConnersHua直连碎片

**介绍：**

​	分门别类，注释的还是很清除的

​	亮点是有特殊直连域名 需要放拦截列表前面

| 文件         | 类型 | 解释                                            |
| ------------ | :--- | ----------------------------------------------- |
| China.list   | 直连 | 常见直连域名                                    |
| Unbreak.list | 直连 | 需要特殊放行的几个域名<br/>一般放在拦截列表前面 |



###  使用建议

​	一定注意好排放顺序，重复度很高的类型碎片，选择一个即可。

​	轻度使用的，没必要放太多，最后可以交给GEO IP 兜底即可

​	本地局域网放前面-》特殊直连域名(主要防止跟拦截冲突，提前放行)-》普通直连域名-》IP段或者GEO



**轻度使用：**

​	LocalAreaNetwork.list + ChinaDomain.list + ChinaCompanyIp.list + GEO CN



**中度使用：**

​	 LocalAreaNetwork.list + GoogleCN.list + Unbreak.list +

​	Special.list + ChinaDomain.list + ChinaCompanyIp.list + GEO CN



**究极使用：**

​	LocalAreaNetwork.list + GoogleCN.list + Unbreak.list +

​	Special.list + ChinaDomain.list + ChinaCompanyIp.list + ChinaIp.list + GEO CN




## 2.4 代理

​	主要分为这几类：本地/局域网地址、中国本地IP和域名、国外能直连的IP和域名

### ACL4SSR代理碎片


**介绍：**

​	如果你所在地区，DNS劫持不严重的话或者使用不频繁的话，轻量级ProxyLite列表足够
​	如果追求列表十分全，可以使用ProxyGFWlist。
​	ProxyGFWlist包含全部的ProxyLite列表
​	ProxyGFWlist = GFWlist + ProxyLite	

| 文件              | 类型          | 解释                                             |
| ----------------- | ------------- | ------------------------------------------------ |
| ProxyLite.list    | 规则碎片-代理 | 比较精简的代理列表，包含常用的，以及被污染的域名 |
| ProxyGFWlist.list | 规则碎片-代理 | GFW的全量列表                                    |
| Telegram.list     | 代理          | Telegram域名和IP段                               |



### lhie1代理碎片

**介绍：**

​	代理规则比较全，另外还有国外视频、Telegram

| 文件          | 类型 | 解释                                             |
| ------------- | :--- | ------------------------------------------------ |
| Proxy.list    | 代理 | 比较精简的代理列表，包含常用的，以及被污染的域名 |
| GlobalTV.list | 代理 | 国外常见视频列表                                 |
| Telegram.list | 代理 | Telegram域名和IP段                               |



### ConnersHua的代理碎片

**介绍：**

​	代理规则比较全，另外还有国外视频、Telegram

| 文件              | 类型 | 解释                                             |
| ----------------- | :--- | ------------------------------------------------ |
| Global.list       | 代理 | 比较精简的代理列表，包含常用的，以及被污染的域名 |
| ForeignMedia.list | 代理 | 国外常见视频列表                                 |
| Telegram.list     | 代理 | Telegram域名和IP段                               |

 

### 使用建议

​	一般使用轻量级的+几个你常用的代理软件的碎片放前面就行 + 兜底代理就行。

​	追求全面的可以把GEW列表加上



**轻度使用：**

​	方案1：ProxyLite.list（acl4ssr） + Telegram.list + 兜底代理

​	方案2：Proxy.list （lhie1）+ Telegram.list + GlobalTV.list （lhie1） + 兜底代理

​	方案3：Global.list （ConnersHua）+ Telegram.list + ForeignMedia.list（ConnersHua） + 兜底代理



**重度使用：**

​	方案1：ProxyGFWlist.list（acl4ssr） + Telegram.list  + 兜底代理

​	方案2：ProxyGFWlist.list （acl4ssr）+ Telegram.list + GlobalTV.list （lhie1） + 兜底代理

​	方案3：ProxyGFWlist.list （acl4ssr）+ Telegram.list + ForeignMedia.list（ConnersHua） + 兜底代理

 

## 2.5 其他规则

​	除了一些代理直连啥的规则，还有一些根据个人喜好，喜欢独立出来的规则

​	比如奈飞分组、Telegram分组、苹果、微软、OneDrive等分组。

​	那些根据自己喜欢放在一般直连或者普通代理列表上面就行。

​	怎么寻找：上上面3个规则里面，如果找到我没介绍的，但是你又很眼熟的，差不多就是你要选择的独立碎片



# 3. 定制规则

## 3.1 规则顺序

​	一般分为规则集合和分组集合，

​	规则顺序是跟网址的匹配顺序有关，放在前面的最先匹配上。

​	匹配上才看规则后面跟的分组集合是谁。

​	综上所述：规则顺序决定你的代理匹配直连，分组顺序无所谓看个人喜好



**规则顺序**

​	自上往下排列（核心思想是避免冲突，该代理的代理、该直连直连）

​	同一分组内的顺序可以随便换，看你自身看中程度。

​	用的着的就加，用不着的就看心情。

​	下面的规则顺序，也不是绝对，

​	同时看上面的**使用建议**



**1.0 局域网地址（必须有，一般直连）**

​	LocalAreaNetwork.list



**2.0 去广告（可选，看自身使用情况）**

​	BanAD.list ( acl4ssr 10分推荐)

​	BanProgramAD.list  ( acl4ssr  10分推荐)

​	BanEasyListChina.list  ( acl4ssr 5分推荐)

​	Reject.list (lhie1)



**2.1 特殊直连域名（可选，看自身使用情况）**

​	GoogleCN.list （能直连的谷歌域名）

​	AsianTV.list	 (lhie1)

​	Special.list  (lhie1,喜欢用BT下载的推荐)

​	Netease Music.list (lhie1，用网易云会员破解的加上)

​	Unbreak.list（ConnersHua）

​	你自己的规则碎片（放这比较好）



**2.2 特殊代理域名（可选，看自身使用情况）**	

​	Netflix.list ( acl4ssr )

​	OneDrive.list ( acl4ssr )	

​	GlobalTV.list  (lhie1)

​	AppleNews.list（ConnersHua）

​	HKMTMedia.list（ConnersHua）

​	你自己的规则碎片（放这比较好）



**2.3 即可直连也可代理的（可选，看自身使用情况）**

​	Microsoft.list ( acl4ssr )

​	Steam.list (lhie1)

​	Apple.list（ConnersHua）

​	Apple.list ( lhie1)



**3.0 一般代理域名**（一般要加）

​	ProxyLite.list( acl4ssr 10分推荐)

​	ProxyGFWlist.list( acl4ssr 7分推荐)



**4.0 一般直连域名**（一般要加）

​	ChinaDomain.list ( acl4ssr 10分推荐)

​	ChinaCompanyIp.list ( acl4ssr 10分推荐)

​	ChinaIp.list ( acl4ssr 3分推荐)

​	China.list（ConnersHua）



**5.0 GEO IP定位**

​	GEOIP,CN 直连（10分推荐）

​	GEOIP,JP 代理（举个例子，不推荐）



**6.0 兜底策略**

​	FINAL 一般兜底代理 (10分推荐)

​	用GFW的可以选择兜底直连 (5分推荐)



## 3.2 寻找规则

### 在线规则

​	找到只显示规则内容的URL就行

​	GitHub举例：

​		打开https://github.com/ACL4SSR/ACL4SSR/blob/master/Clash/ProxyLite.list

​		看到规则列表右上角有几个小按钮，点击Raw，会转跳到一个新网址(raw.githubusercontent.com)。那个网址就是你真正的网址

https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/ProxyLite.list



### 本地规则

​	以subconverter为例，自己找个文件夹，建立一个文本文件，记事本打开，编写规则即可，语法的话，可以阅读对应文档和实例。



## 3.3 编写规则

​	仅做实例，不提供具体教程，自己看网址clash目录/config目录下 有大量的示例

​	本地地址和在线地址可以混揉在一起。



**本地规则**

```
[custom]
;不要随意改变关键字，否则会导致出错
;acl4SSR规则

;去广告：支持
;自动测速：支持
;微软分流：不支持
;苹果分流：不支持
;增强中国IP段：不支持
;增强国外GFW：不支持

surge_ruleset=🎯 全球直连,rules/ACL4SSR/Clash/LocalAreaNetwork.list
surge_ruleset=🛑 全球拦截,rules/ACL4SSR/Clash/BanAD.list
surge_ruleset=🛑 全球拦截,rules/ACL4SSR/Clash/BanProgramAD.list
surge_ruleset=🎯 全球直连,rules/ACL4SSR/Clash/GoogleCN.list
surge_ruleset=🚀 节点选择,rules/ConnersHua/Surge/Ruleset/GlobalMedia.list
surge_ruleset=🚀 节点选择,rules/ConnersHua/Surge/Ruleset/Telegram.list
surge_ruleset=🚀 节点选择,rules/ACL4SSR/Clash/ProxyLite.list
surge_ruleset=🎯 全球直连,rules/ACL4SSR/Clash/ChinaDomain.list
surge_ruleset=🎯 全球直连,rules/ACL4SSR/Clash/ChinaCompanyIp.list
surge_ruleset=🎯 全球直连,[]GEOIP,CN
surge_ruleset=🐟 漏网之鱼,[]FINAL

custom_proxy_group=🚀 节点选择`select`[]♻️ 自动选择`[]🎯 全球直连`.*
custom_proxy_group=♻️ 自动选择`url-test`.*`http://www.gstatic.com/generate_204`300
custom_proxy_group=🎯 全球直连`select`[]DIRECT
custom_proxy_group=🛑 全球拦截`select`[]REJECT`[]DIRECT
custom_proxy_group=🐟 漏网之鱼`select`[]🚀 节点选择`[]🎯 全球直连`[]♻️ 自动选择`.*

enable_rule_generator=true
overwrite_original_rules=true
```

**在线规则**

```
[custom]
;不要随意改变关键字，否则会导致出错
;acl4SSR规则-在线更新版

;去广告：支持
;自动测速：支持
;微软分流：支持
;苹果分流：支持
;增强中国IP段：不支持
;增强国外GFW：不支持

surge_ruleset=🎯 全球直连,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/LocalAreaNetwork.list
surge_ruleset=🛑 全球拦截,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/BanAD.list
surge_ruleset=🍃 应用净化,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/BanProgramAD.list
surge_ruleset=Ⓜ️ 微软服务,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/Microsoft.list
surge_ruleset=🍎 苹果服务,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/Apple.list
surge_ruleset=🌍 国外媒体,rules/ConnersHua/Surge/Ruleset/GlobalMedia.list
surge_ruleset=📲 电报信息,rules/ConnersHua/Surge/Ruleset/Telegram.list
surge_ruleset=🎯 全球直连,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/GoogleCN.list
surge_ruleset=🚀 节点选择,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/ProxyLite.list
surge_ruleset=🎯 全球直连,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/ChinaDomain.list
surge_ruleset=🎯 全球直连,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/ChinaCompanyIp.list
surge_ruleset=🎯 全球直连,[]GEOIP,CN
surge_ruleset=🐟 漏网之鱼,[]FINAL

custom_proxy_group=🚀 节点选择`select`[]♻️ 自动选择`[]🎯 全球直连`.*
custom_proxy_group=♻️ 自动选择`url-test`.*`http://www.gstatic.com/generate_204`300
custom_proxy_group=🌍 国外媒体`select`[]🚀 节点选择`[]♻️ 自动选择`[]🎯 全球直连`.*
custom_proxy_group=📲 电报信息`select`[]🚀 节点选择`[]🎯 全球直连`.*
custom_proxy_group=Ⓜ️ 微软服务`select`[]🎯 全球直连`[]🚀 节点选择`.*
custom_proxy_group=🍎 苹果服务`select`[]🚀 节点选择`[]🎯 全球直连`.*
custom_proxy_group=🎯 全球直连`select`[]DIRECT
custom_proxy_group=🛑 全球拦截`select`[]REJECT`[]DIRECT
custom_proxy_group=🍃 应用净化`select`[]REJECT`[]DIRECT
custom_proxy_group=🐟 漏网之鱼`select`[]🚀 节点选择`[]🎯 全球直连`[]♻️ 自动选择`.*

enable_rule_generator=true
overwrite_original_rules=true
```



# 4. 问题答疑



**我在用啥规则？**

​	ACL4SSR\Clash\config下的mini规则

​	外加去广告的DNS

​	浏览器用ABP去广告扩展

​	手机用 第三方已经魔改过的APP

​	

**去广告有意义么？**

​	看个人喜好，过犹不及。

​	如果不影响正常使用，还能去掉广告，更好。

​	别为了去掉全部广告，影响正常使用



**youtube广告能去吗?**

​	类似于xxx广告能去吗？都是一个套路

​	因为类似于clash和ssr 是基于域名和ip屏蔽的。

​	如果该软件的广告是用了单独域名，是能可以去掉的

​	如果广告是跟正常内容的域名用的是一个的话。那么屏蔽广告的同时也会把正常内容一块屏蔽了。

​	所以一般有些广告是很难通过屏蔽域名去掉的。

​	如果你用的软件支持MITM的话，应该可以，但是需要独立编写规则



**规则越多越好吗？**

​	以现代化电脑来说，规则几千条和几万条，对性能来说，没啥肉眼可见的变化。

​	一般来说不超过1万条就行。

​	如果用在线转换的话，最好少点，要不文件过大，下不下来容易导致超时。

​	避免相同种类用多份，比如有了GEOIP,CN 还要加 ChinaIp




**版权所有，所有内容全部一个个字码出来的，转载必须说明来源**
