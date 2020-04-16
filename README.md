krddy.com-2020
=============

凯瑞达中文官网2020年版


域名绑定、301转向及nginx配置
-----

新建配置文件: ``sudo nano /etc/nginx/sites-available/krddy.com``

编辑配置文件及保存: 

    server {
      listen 443 ssl http2;
      server_name www.krddy.com;
      ssl_certificate krddy.pem;
      ssl_certificate_key krddy.key;
      index index.html;
      root /srv/krddy.com-2020/_site;
      error_page 404 /Error.html;
      add_header Strict-Transport-Security "max-age=15768000" always;
      ssl_protocols TLSv1 TLSv1.1 TLSv1.2 TLSv1.3;
      ssl_ciphers HIGH:!aNULL:!MD5:!DH;
    }
    server {
        listen 443 ssl http2;
        server_name krddy.com;
        ssl_certificate krddy.pem;
        ssl_certificate_key krddy.key;
        return 301 https://www.krddy.com$request_uri;
    }
    server {
        listen 80;
        server_name krddy.com www.krddy.com;
        return 301 https://www.krddy.com$request_uri;
    }

建立链接: ``sudo ln -s /etc/nginx/sites-available/krddy.com /etc/nginx/sites-enabled/``

重启nginx: ``sudo service nginx restart``


下载及生成网站
-----

1. 下载网站源码: ``git clone git://github.com/zackwong/krddy.com-2020.git``

2. 进入源码根目录: ``cd krddy.com-2020``

3. 生成网站: ``jekyll build``


开发者
---------

* Zack Wong &lt;hzzzoo@126.com&gt;

