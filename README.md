## 基于 Ghost
ghost 就是一个博客系统，不走 workpress 的老路子，没有乱七八糟的功能。

## 运行在 Docker 上

1. [ghost汉化的代码这在里](https://github.com/zhimei360/Ghost/tree/zhimei)
1. web 服务器使用 `nginx`
2. 数据库使用 `postgresql`
3. 使用 `docker-compose` 将所有的 `docker` 容器链接起来

## 目录结构

```
blog 
  |-- data ## 存放生产数据的目录，在 docker-compose.yml 有相关装载的指令。
        |-- ghost 
              |-- config  ## ghost 配置文件
              |-- content ## blog 皮肤等文件
        |-- postgres      ## 数据库文件
  |-- ghost    ## 定义 ghost image
  |-- nginx    ## 定义 nginx image
  |-- postgres ## 定义 postgres image
```

为了汉化和替换原代码对 `fonts.googleapi.com` 的依赖，在运行 `ghost` 的容器时遇到了一个坑， `ghost` 的原码中并没有这个文件： `ghost/core/server/views/default.hbs`（管理后台的界面就是这个文件），但是一运行 `ghost` 这个容器，这个文件就会幽灵般自动加载进去。最后也不知道问题出现在哪，只能在原码上创建这个文件覆盖它了。 

## 邮件系统
使用 [QQ企业邮箱](http://exmail.qq.com)，所有邮件由`dev@zhimei360.com`发送。
## 跑起来
想让它跑起来，仅需一行命令
```
$ docker-compose up -d
```
