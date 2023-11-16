安装tuic

~~~
apt -y update && apt -y install wget socat uuid-runtime && wget -O /usr/local/bin/tuic https://github.com/EAimTY/tuic/releases/download/tuic-server-1.0.0/tuic-server-1.0.0-x86_64-unknown-linux-gnu && chmod +x /usr/local/bin/tuic
~~~

下载配置文件

~~~
wget -O /usr/local/etc/config.json https://github.com/dandan1394/ziyong/blob/main/config.json && wget -P /etc/systemd/system https://github.com/dandan1394/ziyong/blob/main/tuic.service
~~~

安装ACME
~~~
curl https://get.acme.sh | sh
~~~


设置ACME别名
~~~
alias acme.sh=~/.acme.sh/acme.sh
~~~

自动更新ACME
~~~
acme.sh --upgrade --auto-upgrade
~~~

设置ACME默认CA
~~~
acme.sh --set-default-ca --server letsencrypt
~~~
生成证书
~~~
acme.sh --issue -d www.example.com --standalone -k ec-256 --webroot /home/wwwroot/html
~~~
安装证书
~~~
acme.sh --install-cert -d www.example.com --ecc --key-file /etc/ssl/private/private.key --fullchain-file /etc/ssl/private/cert.crt
~~~
修改配置文件
~~~
uuidgen
~~~
生成密码
~~~
openssl rand -base64 32
~~~
重启查看运行状态
~~~
systemctl daemon-reload && systemctl enable --now tuic.service && systemctl status tuic.service
~~~
