# 常用命令与环境

### 一 : apt-get

`apt-get install`

```shell 1.下载的软件存放位置
1.下载的软件存放位置
/var/cache/apt/archives
2.安装后软件默认位置
/usr/share
3.可执行文件位置 
/usr/bin
4.配置文件位置
/etc
5.lib文件位置
/usr/lib

```

 

### 二:防火墙iptables

ubuntu 默认安装是无环境的,但事实环境防火墙也是启动了

`iptables -P INPUT ACCEPT`

`iptables -P FORWARD ACCEPT`



