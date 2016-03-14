nginx + uwsgi + flask!
===================
----------
#### <i class="icon-refresh"></i> CentOS 7 install Nginx

> **方法一:yum安装**

> - sudo yum install epel-release
> - sudo yum install nginx
> - sudo systemctl start nginx.service

> **方法二:自编译安装**
> - 参考[here](https://www.nginx.com/resources/wiki/start/topics/tutorials/install/)

----------
#### <i class="icon-refresh"></i> install and config mariadb
> **安装**
>- sudo yum install mariadb-server
> **配置**
> - vi /etc/my.ini    在[mysqld]在增加一行
> - character-set-server=utf8
> **启动**
> - systemctl start mariadb.service
> **配置root密码和是否远程**
> - mysql_secure_installation

----------
#### <i class="icon-refresh"></i> virtualenv & flask project
```
## install plugin
sudo easy_install pip
sudo pip install virtualenv
mkdir workspace
cd workspace/
virtualenv insomnia
source insomnia/bin/activate(执行后变化(insomnia)[datacenter@localhost workspace]$)
## 安装依赖
pip install Flask Flask-Script Flask-SQLAlchemy Flask-Restless flask-excel pyexcel pyexcel-xls pyexcel-xlsx simplejson uwsgi
```
> **Tip:** Error **ImportError: No module named MySQLdb** ----> **Slove:** 
> - sudo yum install MySQL-python
> - sudo yum install python-devel mysql-devel
> - git clone https://github.com/jehiah/mysql-python.git
> - cd mysql-python
> - python setup.py build
> - python setup.py install (virtualenv 下不需要sudo)


### nginx config

> **在/etc/nginx/conf.d新建XXX.conf,写入如下内容：**
```
server {
  listen       8000;
  server_name  xiejdm;
  location / {
    include uwsgi_params;
    uwsgi_pass 127.0.0.1:8002
    try_files $uri $uri/ =404;
  }    
  location /static {
    root   /home/datacenter/workspace/Insomnia/App;
  }    
}
```
----------
### Support by Gideon Xie

> **E-mail:** [xiejdm@gmail.com](mailto:xiejdm@gmail.com)    **Tel:**010-64089654
