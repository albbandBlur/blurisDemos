### 搭建可控制权限的Git仓库

> 由于git没有自带的仓库权限控制，但提供了hooker函数，因此可以自己编写脚本进行权限控制。有开源项目`gitolite`已实现分支级权限控制的功能可以直接使用。

1. 安装Git

2. 创建Git仓库管理员账号：`useradd git`

3. 切换到Git仓库管理员账号：`su git`

4. 确认在Git仓库管理的主目录下没有`.ssh/authorized_key`文件的存在

5. 获取`gitolite`版本库并安装

   1. `git clone https://github.com/sitaramc/gitolite ~/`
   2. 在Git仓库管理员主目录下创建bin目录并安装
      1. `mkdir ~/bin`
      2. `~/gitolite/install -to ~/bin`

6. 配置gitolite管理员

   > gitolite 使用特殊的版本库gitolite-admin 来管理用户和版本库，所以需要创建一个管理员来管理所有的用户和版本库

   1. 使用Git仓库管理员账号，且在Git仓库管理员的主目录下执行以下命令生产公私秘钥：`ssh-keygen -t rsa`

   2. 将生成的公钥改名为`admin.pub`

      > .pub之前的就是用户名，可根据需求修改

   3. 使用管理员公钥安装gitolite：~/bin/gitolite setup -pk ~/.ssh/admin.pub

   4. 在Git仓库管理员主目录下生成管理员管理仓库（不需要输密码）：

      `git clone git@127.0.0.1:gitolite-admin.git`

      > 进入仓库后可以看到conf 和keydir 
      >
      > conf/gitolite.conf 是添加用户/仓库的配置 
      >
      > keydir 是放对应用户的公钥
      >
      > 并且此时，admin.pub这个公钥可以删除了

7. 创建项目

   1. 添加项目，编辑管理员管理仓库下的`config/gitolite.conf`：

      ```shell
      ###定义用户组
      @admin = admin
      @user = tao wjwen song
      
      ###git管理员仓库
      repo gitolite-admin
          RW+     =   admin
      
      ###git项目
      repo testing
          RW+     =   @all
      
      repo nuode
          RW+     =   @user
      ```

      > 可添加多个用户组，格式：@用户组名 = 用户1 用户2 用户3
      >
      > 可添加多个git项目仓库，格式：
      >
      > repo 仓库名
      >
      > ​	权限	=	@用户组/用户名

   2. 添加用户，编辑管理员管理仓库下的`keydir`：

      > 在此目录下添加项目成员的公钥key，命名规则为：用户名.pub，用户名即对应上述仓库配置文件中的用户名

   3. 提交修改：

      1. 在管理员管理仓库下执行提交修改操作：

         1. `git add .`

         2. `git commit -am "create new project"`

            > 可能执行本地提交后会提醒需要设置用户名和邮件地址，执行以下命令：
            >
            > `git config --global user.name 用户名`
            >
            > `git config --global user.email 邮件地址`

         3. `git push`

            > 可能会提示没有默认提交的设置，执行以下命令：
            >
            > `git config --global push.default simple`

      2. 提交完修改后，在`~/repositories/`目录下会多出刚刚添加的项目仓库，此时已创建成功，可以给项目成员使用。

      3. git的克隆地址为：git clone Git仓库管理员账号名@服务器ip地址:项目仓库名.git