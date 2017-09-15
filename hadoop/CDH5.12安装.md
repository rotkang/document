# 系统环境配置 #

```
**操作系统**
CentOS 7.3.1611

**IP地址分配** 
192.168.136.11 cdh1.localdomain cdh1
192.168.136.12 cdh2.localdomain cdh2
192.168.136.13 cdh3.localdomain cdh3

**硬件配置** 
4 Cores,4G Memory,40G Disk 
```

# 安装前工作 #

参考官网手册：https://www.cloudera.com/downloads/cdh/5-12-0.html

1. 检查防火墙是否开启

1.1. 检查防火墙是否开启：`firewall-cmd --state`

1.2. 停止防火墙：`systemctl stop firewalld.service` 

1.3. 禁止开机启动防火墙：`systemctl disable firewalld.service` 

1.4. 关闭SELINUX： `sed -i "s/SELINUX=enforcing/SELINUX=disabled/" /etc/selinux/config`

1.5. 重启`reboot`

2. 检查网络是否畅通

3. 配置SSH无密登录

3.1. 生成密钥(可一直回车)：`ssh-keygen -b 1024 -t rsa`

3.2. 管理密钥：`cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys`

3.3. 远程拷贝：`scp ~/.ssh/authorized_keys userName@hostName:~/.ssh/authorized_keys`

如果使用root无密登录修改vi /etc/ssh/sshd_config中的`PermitRootLogin yes` `StrictModes no`

4. 检查JDK是否符合版本要求，详见：https://www.cloudera.com/downloads/cdh/5-12-0.html

4.1. 查看系统自带的JDK：`rpm -qa|grep java`

4.2. 卸载系统自带的JDK：`rpm -e --nodeps java-1.8.0-openjdk-headless-1.8.0.102-4.b14.el7.x86_64|java-1.8.0-openjdk-1.8.0.102-4.b14.el7.x86_64`

4.3. 安装JDK，配置JDK环境变量。`vi /etc/profile`

`JAVA_HOME=/usr/app/java/jdk1.8.0_111`

`JRE_HOME=/usr/app/java/jdk1.8.0_111/jre`

`PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin`

`CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib`

`export JAVA_HOME JRE_HOME PATH CLASSPATH`

4.4. source /etc/profile

5. 安装NTP服务

5.1. 所有节点服务器：`yum -y install ntp`

5.2. 重新指定同步时间：cdh1服务器不动使用默认指定，其它cdh2,cdh3修改成：`server cdh1 iburst`

5.3 `systemctl start ntpd`

5.4 `systemctl enable ntpd`



# Cloudera Manager安装 #
