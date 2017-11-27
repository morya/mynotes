# ubuntu 14 安装gitlab

-   安装ubuntu 操作系统
    除了 openssh server 其它都不需要
-   配置软件源

```
root@gitlab:~# cat /etc/apt/sources.list
deb http://mirrors.sohu.com/ubuntu/ trusty multiverse universe restricted main
deb http://mirrors.sohu.com/ubuntu/ trusty-updates multiverse universe restricted main
deb http://mirrors.sohu.com/ubuntu/ trusty-backports multiverse universe restricted main
deb http://mirrors.sohu.com/ubuntu/ trusty-security multiverse universe restricted main
deb http://mirrors.sohu.com/ubuntu/ trusty-proposed multiverse universe restricted main
```

-   配置Gitlab源

[详细步骤](https://mirror.tuna.tsinghua.edu.cn/help/gitlab-ce)

```
# 简单说明
curl https://packages.gitlab.com/gpg.key 2> /dev/null | sudo apt-key add - &>/dev/null

echo 'deb https://mirrors.tuna.tsinghua.edu.cn/gitlab-ce/ubuntu trusty main' >> /etc/apt/sources.list.d/gitlab-ce.list
```

-   执行update

```
apt-get update
apt-get install gitlab-ce

# 也可以选择安装特定版本
apt-get install gitlab-ce=8.9.6-ce.0
# 这个特定版本是我备份gitlab时候用到的版本
```

-   配置gitlab

```
gitlab-ctl reconfigure
```

-   [配置gitlab 使用qq 企业邮箱](http://www.ttlsa.com/linux/howto-gitlab-using-qq-mailserver-send-mail/)

```
# vim /etc/gitlab/gitlab.rb
gitlab_rails['smtp_enable'] = true
gitlab_rails['smtp_address'] = "smtp.exmail.qq.com"
gitlab_rails['smtp_port'] = 465
gitlab_rails['smtp_user_name'] = "support@ttlsa.com"
gitlab_rails['smtp_password'] = "www.ttlsa.com"
gitlab_rails['smtp_domain'] = "ttlsa.com"
gitlab_rails['smtp_authentication'] = "login"
gitlab_rails['smtp_enable_starttls_auto'] = true
gitlab_rails['smtp_tls'] = true
gitlab_rails['gitlab_email_from'] = "support@ttlsa.com"
```

-   再次执行 `gitlab-ctl reconfigure`
