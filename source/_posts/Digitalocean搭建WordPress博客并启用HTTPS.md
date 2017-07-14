---
title: Digitalocean搭建WordPress博客并启用HTTPS
date: 2017-07-14 11:09:42
tags:
---
#### [注册Digtalocean](https://m.do.co/c/382409e24e05)
#### 一键搭建WordPress
[how-to-use-the-wordpress-one-click-install-on-digitalocean](https://www.digitalocean.com/community/tutorials/how-to-use-the-wordpress-one-click-install-on-digitalocean)
#### 启用BBR加速（By teddysun）
```Bash
wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh
chmod +x bbr.sh
./bbr.sh
```
<!--more-->
#### 使用acme.sh签发Let's Encrypt免费ECC SSL证书
[我是照着这篇文章做的](https://yjk.im/le-ecc-ssl/)
#### WordPress强制HTTPS
##### Apache2开启ssl和rewrite
`a2enmod ssl`  
`a2enmod rewrite`  
`service apache2 restart`
##### 编辑配置文件
`vi /etc/apache2/sites-available/default-ssl.conf`
```Bash
<IfModule mod_ssl.c>
    <VirtualHost _default_:443>
        ServerAdmin admin@example.com
        ServerName your_domain.com
        ServerAlias www.your_domain.com
        DocumentRoot /var/www/html
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
        SSLEngine on
        SSLCertificateFile /Let's Encrypt证书位置
        SSLCertificateKeyFile /Let's Encrypt证书KEY位置
        <FilesMatch "\.(cgi|shtml|phtml|php)$">
                        SSLOptions +StdEnvVars
        </FilesMatch>
        <Directory /usr/lib/cgi-bin>
                        SSLOptions +StdEnvVars
        </Directory>
        BrowserMatch "MSIE [2-6]" \
                        nokeepalive ssl-unclean-shutdown \
                        downgrade-1.0 force-response-1.0
        BrowserMatch "MSIE [17-9]" ssl-unclean-shutdown
    </VirtualHost>
</IfModule>
```
`vi /etc/apache2/sites-available/000-default.conf`
```Bash
RewriteEngine on
RewriteCond %{SERVER_PORT} !^443$
RewriteRule ^(.*)?$ https://%{SERVER_NAME}/$1 [L,R]
```
`service apache2 restart`
##### 在WordPress的设置里面填写你的HTTPS域名完工