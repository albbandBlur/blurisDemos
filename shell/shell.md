### shell常用写法

#### 1.基础

```shell
1.编写shell 后缀使用 .shell
2.开头编写#!/bin/bash
3.给予权限chmod +x ./执行shell
4.#单行注释
5.:<<!多行注释!
6.cut
```

#### 2.初步编写

###### 1.使用for循环在/oldboy目录下批量创建10个html文件，其中每个文件需要包含10个随机小写字母加固定字符串oldboy

``` shell
#!/bin/bash
[ -d /home/wwwroot/shell ] || mkdir /home/wwwroot/shell
cd /home/wwwroot/shell

for i in {1..10}
do
filename=$(uuidgen|tr '0-9' 'a-z'|cut -c 1-10 )
touch ${filename}_oldboy.html
done

第一句[ -d /home/wwwroot/shell ] -d查询这个目录是否存在 或 直接创建
-e filename 	如果 filename存在，则为真 	
-d filename 	如果 filename为目录，则为真 
-f filename 	如果 filename为常规文件，则为真 	
-L filename 	如果 filename为符号链接，则为真 	
-r filename 	如果 filename可读，则为真 	
-w filename 	如果 filename可写，则为真 	
-x filename 	如果 filename可执行，则为真 

shell 的for 循环
for i in (循环体)
do
循环内容
done

1.{1..10} 循环十次
2.filename=$(uuidgen|tr '0-9' 'a-z'|cut -c 1-10 )

uuidgen|tr '0-9' 'a-z' 随机输出
|cut -c 1-10 输出1到10个
```



###### 2.结果文件名中的oldboy字符串全部改成oldgirl(最好用for循环实现),并且将扩展名html全部改成大写。

```shell
#!/bin/bash
[ -d /home/wwwroot/shell ] || mkdir /home/wwwroot/shell
cd /home/wwwroot/shell

for i in $(ls *html)
do
rankStr = $(echo $i|cut -c 1-10)
mv $i ${randStr}_oldgirl.HTML
done

1.先去到shell 下列出 ls *html的文件
2.cut之前的name 获取1-10总共10位
3.修改原先的 改为 ${randStr}拼接


```

