# 卸载不要的环境

杀掉不需要的进程

卸载不要的安装包

`rem -qa | grep mysql | xargs yum -y remove`

`ls /etc/my.cnf`  这个可以直接备份

`ls /var/lib/mysql/`



# 获取mysql官方yum源

`cat /etc/redhat-release` 查看自己系统的版本信息

下载rpm安装包 官网下或者wget

`ls /etc/yum.repos.d/ -l` 查看yum源

rpm -ivh 安装rpm安装包 更新yum源



# 安装完成

![image-20231118153649455](https://crush-blog.oss-cn-hangzhou.aliyuncs.com/blog/202311181537609.png)



# 登录

vim /etc/my.cnf

skip-grant-tables

可以跳过密码验证

当然也可以自己设置密码



# 配置文件

vim /etc/my.cnf



设置开机自启

systemctl enable

systemctl daemon-relaod



设置字符集？

