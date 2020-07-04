# 原ACL规则https://github.com/ACL4SSR/ACL4SSR 基于此规则按个人习惯二次修改
## 已修改内容如下：
### 20200630
#### 新增GameDownload.list，整合四大平台的下载规则
#### 新增GamePlatform.list，整合四大平台的规则（不包含下载）
#
# 目前Clash支持的规则类型如下：
* DOMAIN-SUFFIX：域名后缀匹配
* DOMAIN：域名匹配
* DOMAIN-KEYWORD：域名关键字匹配
* IP-CIDR：IP段匹配
* SRC-IP-CIDR：源IP段匹配
* GEOIP：GEOIP数据库（国家代码）匹配
* DST-PORT：目标端口匹配
* SRC-PORT：源端口匹配
* MATCH：全匹配（一般放在最后）
