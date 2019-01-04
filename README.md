> 自用php镜像 封装常用扩展

> FPM docker: docker push shanliu/php:fpm

> CLI docker: docker push shanliu/php:cli



> 关于基于官方PHP的dockerfile支持以下命令备注:
```
docker-php-source extract #解压PHP源码
docker-php-ext-install yaf #安装扩展,前提是先下载扩展到ext目录,pecl库可以通过 pecl bundle yaf 下载
docker-php-ext-configure gd  --with-jpeg-dir=/usr/include/  --with-freetype-dir=/usr/include/ #扩展安装时的配置编译参数命令
```
