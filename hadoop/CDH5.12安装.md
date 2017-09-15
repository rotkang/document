# 系统环境配置 #

```
**操作系统**
CentOS 7.3.1611

**IP地址分配** 
192.168.136.11 cdh1 cdh1.localdomain
192.168.136.12 cdh2 cdh2.localdomain
192.168.136.13 cdh3 cdh3.localdomain

**硬件配置** 
4 Cores,4G Memory,40G Disk 
```

# 安装前工作 #

参考官网手册：https://www.cloudera.com/downloads/cdh/5-12-0.html

1. 检查防火墙是否开启

检查防火墙是否开启：`firewall-cmd --state`

停止防火墙：`systemctl stop firewalld.service` 

禁止开机启动防火墙：`systemctl disable firewalld.service` 

2. 检查网络是否畅通

3. 配置SSH无密登录

生成密钥(可一直回车)：`ssh-keygen -b 1024 -t rsa`

管理密钥：`cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys`

远程拷贝：`scp ~/.ssh/authorized_keys userName@hostName:~/.ssh/authorized_keys`

如果使用root无密登录修改vi /etc/ssh/sshd_config中的`PermitRootLogin yes` `StrictModes no`

4. 检查JDK是否符合版本要求，详见：https://www.cloudera.com/downloads/cdh/5-12-0.html

# Cloudera Manager安装 #
