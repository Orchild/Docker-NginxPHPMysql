# Docker-NginxPHPMysql
用docker-compose初始化Nginx，PHP，Mysql

## 注意
- 项目中各处权限映射为主机UID为1000用户
- 用link连接容器时，已为各个容器生成相应IP，mysql，redis应使用对应IP作为host IP
