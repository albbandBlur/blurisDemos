

																[回到目录](../index.md)

## 常用命令：

git 初始化：`git init` 

更新：`git pull `

提交sta
1.  加入未受版本库控制的加入：` git add . `
2. 提交至仓库。不设置默认为本地仓库：`  git commit -am "update"  ` 
3. 提交至git服务器上：`git push origin xxx  `

提交end



查看分支：	`git branch -a`

创建分支：	  `git branch 分支名`

切换分支：	  `git checkout 分支名`

删除本地分支 ：`git branch -D 分支名`

删除远程分支： `git push origin :分支名`

更新分支： `git fetch`



## **合并分支**

先切换分支。切换到你要更新的分支 `git pull`

`git merge` 需要合并的分支

`git push`	提交代码 

切换回原分支



To:如果切换失败使用 更新分支：



## **基础配置：**

```shell
git config --global user.name "用户名" 

git config --global user.email "邮箱地址"

ssh-keygen -t rsa -C "邮箱地址"

git config user.name 查看本机用户 

git config user.email 查看本机email

git config --global user.name "username" 修改用户 

git config --global user.email "email" 修改email

```



## **服务添加新的项目：**

```shell
su git 切换git用户

cd ~ 去到主目录
vi gitolite-admin/conf/gitolite.conf

新建组:
repo 仓库名
权限 = @用户组/用户名

和人员名单:
人员名单的私钥。/gitolite-admin/keydir/

新建完毕。

git pull
git add .
git commit -am "update"
git push

```





## **拉取项目：**

`git clone Git仓库管理员账号名@服务器ip地址:项目仓库名.git`



## **缓冲区：**

```shell
如果本地仓库或服务仓库中存在一定的差异。如果是本地传输至服务的。可直接替代

如果其中有差异（超前）、那先去有超前的库中，先缓存git stash （上一次pull 之前）提前的

然后更改版本的差异。提交至超前的版本中

查看后，如果抛弃之前的缓冲 git stash clear  

```



## **回滚版本：**

查看git 日记： `git  log` 			 

回退到上个版本： `git reset --hard HEAD^`         

`git reset --hard HEAD~3`        回退到前3次提交之前，以此类推，回退到n次提交之前

` git reset --hard commit_id`     退到/进到 指定commit的sha码


