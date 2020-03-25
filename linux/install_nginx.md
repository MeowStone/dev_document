#安装nginx

##检查是否已安装nginx所需依赖

通过

    yum list installed gcc

或 

    yum list installed | grep "gcc"

或者忽略以上，直接安装依赖（***yum***自动帮你安装好依赖和依赖所需的依赖，已安装的则更新）：

    yum -y install gcc pcre-devel zlib-devel openssl openssl-devel

输出：

    [root@localhost /]# yum -y install gcc pcre-devel zlib-devel openssl openssl-devel
    Loaded plugins: fastestmirror, langpacks
    Loading mirror speeds from cached hostfile
     * base: mirrors.nju.edu.cn
     * extras: mirrors.163.com
     * updates: mirrors.nju.edu.cn
    Package 1:openssl-1.0.2k-19.el7.x86_64 already installed and latest version
    Resolving Dependencies

	【忽略大量信息】
    
    Installed:
      gcc.x86_64 0:4.8.5-39.el7openssl-devel.x86_64 1:1.0.2k-19.el7 
      pcre-devel.x86_64 0:8.32-17.el7  zlib-devel.x86_64 0:1.2.7-18.el7 
    
    Dependency Installed:
      cpp.x86_64 0:4.8.5-39.el7 
      glibc-devel.x86_64 0:2.17-292.el7 
      glibc-headers.x86_64 0:2.17-292.el7   
      kernel-headers.x86_64 0:3.10.0-1062.18.1.el7  
      keyutils-libs-devel.x86_64 0:1.5.8-3.el7  
      krb5-devel.x86_64 0:1.15.1-37.el7_7.2 
      libcom_err-devel.x86_64 0:1.42.9-16.el7   
      libselinux-devel.x86_64 0:2.5-14.1.el7
      libsepol-devel.x86_64 0:2.5-10.el7
      libverto-devel.x86_64 0:0.2.5-4.el7   
    
    Dependency Updated:
      krb5-libs.x86_64 0:1.15.1-37.el7_7.2  
      krb5-workstation.x86_64 0:1.15.1-37.el7_7.2   
      libkadm5.x86_64 0:1.15.1-37.el7_7.2   
    
    Complete!

##下载nginx

###下载源码压缩包

    wget -P /usr/local/ http://nginx.org/download/nginx-1.16.1.tar.gz
> 这里使用wget下载 -P(大写) 指定文件存在路径

    [root@localhost /]# wget -P /usr/local/ http://nginx.org/download/nginx-1.16.1.tar.gz
    --2020-03-25 09:27:43--  http://nginx.org/download/nginx-1.16.1.tar.gz
    Resolving nginx.org (nginx.org)... 62.210.92.35, 95.211.80.227, 2001:1af8:4060:a004:21::e3
    Connecting to nginx.org (nginx.org)|62.210.92.35|:80... connected.
    HTTP request sent, awaiting response... 200 OK
    Length: 1032630 (1008K) [application/octet-stream]
    Saving to: ‘/usr/local/nginx-1.16.1.tar.gz’
    
    100%[======================================>] 1,032,630   6.54KB/s   in 2m 46s 
    
    2020-03-25 09:30:30 (6.08 KB/s) - ‘/usr/local/nginx-1.16.1.tar.gz’ saved [1032630/1032630]

###解压源码并编译安装
进入tar.gz文件所在目录

    cd /usr/local/

解压

    tar -zxvf nginx-1.16.1.tar.gz

进入nginx-1.16.1目录

    cd nginx-1.16.1

配置nginx安装目录，可忽略

    ./configure --prefix=/usr/local/nginx

>配置命令输出：

    [root@localhost nginx-1.16.1]# ./configure --prefix=/usr/local/nginx
   
	【忽略一大堆】
 
    Configuration summary
      + using system PCRE library
      + OpenSSL library is not used
      + using system zlib library
    
	[所有相关文件均生成在指定文件夹]
      nginx path prefix: "/usr/local/nginx"
      nginx binary file: "/usr/local/nginx/sbin/nginx"
      nginx modules path: "/usr/local/nginx/modules"
      nginx configuration prefix: "/usr/local/nginx/conf"
      nginx configuration file: "/usr/local/nginx/conf/nginx.conf"
      nginx pid file: "/usr/local/nginx/logs/nginx.pid"
      nginx error log file: "/usr/local/nginx/logs/error.log"
      nginx http access log file: "/usr/local/nginx/logs/access.log"
      nginx http client request body temporary files: "client_body_temp"
      nginx http proxy temporary files: "proxy_temp"
      nginx http fastcgi temporary files: "fastcgi_temp"
      nginx http uwsgi temporary files: "uwsgi_temp"
      nginx http scgi temporary files: "scgi_temp"
    
编译

    make

>输出忽略，太长了

安装

    make install
>安装输出

    [root@localhost nginx-1.16.1]# make install
    make -f objs/Makefile install
    make[1]: Entering directory `/usr/local/nginx-1.16.1'
    test -d '/usr/local/nginx' || mkdir -p '/usr/local/nginx'
    test -d '/usr/local/nginx/sbin' \
    || mkdir -p '/usr/local/nginx/sbin'
    test ! -f '/usr/local/nginx/sbin/nginx' \
    || mv '/usr/local/nginx/sbin/nginx' \
    '/usr/local/nginx/sbin/nginx.old'
    cp objs/nginx '/usr/local/nginx/sbin/nginx'
    test -d '/usr/local/nginx/conf' \
    || mkdir -p '/usr/local/nginx/conf'
    cp conf/koi-win '/usr/local/nginx/conf'
    cp conf/koi-utf '/usr/local/nginx/conf'
    cp conf/win-utf '/usr/local/nginx/conf'
    test -f '/usr/local/nginx/conf/mime.types' \
    || cp conf/mime.types '/usr/local/nginx/conf'
    cp conf/mime.types '/usr/local/nginx/conf/mime.types.default'
    test -f '/usr/local/nginx/conf/fastcgi_params' \
    || cp conf/fastcgi_params '/usr/local/nginx/conf'
    cp conf/fastcgi_params \
    '/usr/local/nginx/conf/fastcgi_params.default'
    test -f '/usr/local/nginx/conf/fastcgi.conf' \
    || cp conf/fastcgi.conf '/usr/local/nginx/conf'
    cp conf/fastcgi.conf '/usr/local/nginx/conf/fastcgi.conf.default'
    test -f '/usr/local/nginx/conf/uwsgi_params' \
    || cp conf/uwsgi_params '/usr/local/nginx/conf'
    cp conf/uwsgi_params \
    '/usr/local/nginx/conf/uwsgi_params.default'
    test -f '/usr/local/nginx/conf/scgi_params' \
    || cp conf/scgi_params '/usr/local/nginx/conf'
    cp conf/scgi_params \
    '/usr/local/nginx/conf/scgi_params.default'
    test -f '/usr/local/nginx/conf/nginx.conf' \
    || cp conf/nginx.conf '/usr/local/nginx/conf/nginx.conf'
    cp conf/nginx.conf '/usr/local/nginx/conf/nginx.conf.default'
    test -d '/usr/local/nginx/logs' \
    || mkdir -p '/usr/local/nginx/logs'
    test -d '/usr/local/nginx/logs' \
    || mkdir -p '/usr/local/nginx/logs'
    test -d '/usr/local/nginx/html' \
    || cp -R html '/usr/local/nginx'
    test -d '/usr/local/nginx/logs' \
    || mkdir -p '/usr/local/nginx/logs'
    make[1]: Leaving directory `/usr/local/nginx-1.16.1'

测试安装是否ok，切换至安装目录

    cd /./usr/local/nginx/

测试 

    ./sbin/nginx -t
>测试输出

    [root@localhost nginx]# ./sbin/nginx -t
    nginx: the configuration file /usr/local/nginx/conf/nginx.conf syntax is ok
    nginx: configuration file /usr/local/nginx/conf/nginx.conf test is successful

###启动nginx

启动

    ./sbin/nginx

使用curl测试

    curl get 127.0.0.1
>输出

    [root@localhost sbin]# curl get 127.0.0.1
    error code: 1003<!DOCTYPE html>
    <html>
    <head>
    <title>Welcome to nginx!</title>
    <style>
    body {
    width: 35em;
    margin: 0 auto;
    font-family: Tahoma, Verdana, Arial, sans-serif;
    }
    </style>
    </head>
    <body>
    <h1>Welcome to nginx!</h1>
    <p>If you see this page, the nginx web server is successfully installed and
    working. Further configuration is required.</p>
    
    <p>For online documentation and support please refer to
    <a href="http://nginx.org/">nginx.org</a>.<br/>
    Commercial support is available at
    <a href="http://nginx.com/">nginx.com</a>.</p>
    
    <p><em>Thank you for using nginx.</em></p>
    </body>
    </html>

控制台已经打印出***nginx***的欢迎页html信息，至此nginx已成功安装完成

###PC访问不到虚拟机的nginx

检查防火墙是否开启80端口

    [root@localhost /]# firewall-cmd --query-port=80/tcp
    no

永久开启80端口

    [root@localhost /]# firewall-cmd --add-port=80/tcp --permanent
    success

重启防火墙

    [root@localhost /]# systemctl restart firewalld