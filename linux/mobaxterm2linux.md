# MobaXterm连接linux虚拟机 #


##开启ssh##

###检测是否安装openssh###
通过yum工具检查linux是否已安装openssh:

    [root@localhost /]# yum list installed openssh
    Loaded plugins: fastestmirror, langpacks  
    Loading mirror speeds from cached hostfile  
     * base: mirrors.aliyun.com  
     * extras: mirrors.cn99.com  
     * updates: mirrors.cn99.com  
    //已安装   
    Installed Packages  
    openssh.x86_64


**如已安装跳过此步骤**

通过yum安装openssh

    yum -y(安装过程中出现y/n默认选择y) install openssh

###检测是否开启ssh###

检查ssh服务状态

    service sshd status

如未启动输出以下信息：

    [root@localhost]# service sshd status  
    Redirecting to /bin/systemctl status sshd.service  
    ● sshd.service - OpenSSH server daemon  
       Loaded: loaded (/usr/lib/systemd/system/sshd.service; disabled; vendor preset: enabled)  
       Active: inactive (dead)  
     Docs: man:sshd(8)  
       man:sshd_config(5)  

若启动，则输出：

    [root@localhost]# service sshd status
    Redirecting to /bin/systemctl status sshd.service
    ● sshd.service - OpenSSH server daemon
       Loaded: loaded (/usr/lib/systemd/system/sshd.service; disabled; vendor preset: enabled)
       Active: active (running) since Wed 2020-03-25 08:54:09 UTC; 2min 41s ago
     Docs: man:sshd(8)
       man:sshd_config(5)
     Main PID: 3024 (sshd)
       CGroup: /system.slice/sshd.service
       └─3024 /usr/sbin/sshd -D
    
    Mar 25 08:54:09 localhost systemd[1]: Starting OpenSSH server daemon...
    Mar 25 08:54:09 localhost sshd[3024]: Server listening on 0.0.0.0 port 22.
    Mar 25 08:54:09 localhost sshd[3024]: Server listening on :: port 22.
    Mar 25 08:54:09 localhost systemd[1]: Started OpenSSH server daemon.


启动ssh服务：

    [root@localhost]# service sshd start
    Redirecting to /bin/systemctl start sshd.service

启动后，再次查看ssh服务状态即显示*active*。


##使用MobaXterm连接linux##

若仍旧显示*connection refused*

###检查linux是否设定初始密码###

若没有密码，切换至root用户：

    su root

为root用户初始化密码：

    passwd root 

输出一下信息：

    [root@localhost /]# passwd root
    Changing password for user root.
    New password: [密码不显示]
    BAD PASSWORD: The password is shorter than 8 characters[警告密码太短，可忽略]
    Retype new password: [密码不显示]
    passwd: all authentication tokens updated successfully.

再次使用MobaXterm连接linux即可。