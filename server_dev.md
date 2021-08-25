# 开服服务器部署程序脚本（拉取git）

## first 服务器记忆账户密码

1.
~~~
cat > git-credentials
http://myname:pwd@118.25.10.36:3100
~~~
2.git config --global credential.helper store 
3.git clone xxx


## second 前端初始化
## 首次部署安装
~~~
WEB='/home/ubuntu/font-web'

cd $WEB &&  docker run --rm -v $WEB:/root  node:12 /bin/bash -c "cd /root && npm install"

~~~



## third 编译
[x]前端
~~~
WEB='/home/ubuntu/font-web'
WEBBUILD='/home/ubuntu/font-web/dist/'
WEBPUB='/home/ubuntu/caddy/www/dist/'

cd $WEB && /usr/bin/git pull && docker run --rm -v $WEB:/root  node:12 /bin/bash -c "cd /root && npm run build" && rsync -a $WEBBUILD $WEBPUB
~~~



## 管理页面
[x]web
~~~
WEB='/home/ubuntu/back/back-web'
WEBBUILD='/home/ubuntu/back/back-web/dist/'
WEBPUB='/home/ubuntu/back/back-api/public/resource'

cd $WEB && /usr/bin/git pull && docker run --rm -v $WEB:/root node:12 /bin/bash -c "cd /root && npm run build:prod" &&   rsync -a $WEBBUILD $WEBPUB
~~~


## api服务 
[ ]
~~~
SERVER='/home/ubuntu/back/back-api'
WEBPUB='/home/ubuntu/gserver/server1/'

cd $SERVER  && rm -r packed && /usr/bin/git pull && docker run --rm -v $SERVER:/root golang:alpine /bin/sh -c "cd /root && GOPROXY=https://goproxy.io,direct  CGO_ENABLED=0 go build -ldflags=\"-s -w\" ." && mv ${!SERVER}/outbin $WEBPUB
~~~
