

# Github的使用--Mac

## 如何查看自己电脑Git是否安装成功

~~~ASN.1
git --version
如果安装成功   git version 2.24.3 (Apple Git-128)
~~~

## 第一步：设定个人消息

~~~ASN.1
$ git config --global user.name "King"//输入姓名
$ git config --global user.email "2457808858@qq.com" //输入个人邮箱 
查询git设定的内容
git config --list

~~~

![截屏2021-05-24 下午9.46.43](/Users/wking/Library/Application Support/typora-user-images/截屏2021-05-24 下午9.46.43.png)

## 查看状态

~~~apl
git status 
~~~

## 将工作区文件添加到暂存区

~~~apl
git add 文件名
~~~

### git commit  -m 主要是将暂存区里的改动给提交到本地的版本库

成功![截屏2021-05-24 下午10.34.41](/Users/wking/Library/Application Support/typora-user-images/截屏2021-05-24 下午10.34.41.png)

### 查看更新记录

~~~apl
git -log
~~~

## 后悔

### 1.将暂存区的文件覆盖到工作目录上 

~~~apl
git checkout 文件名
~~~

---



### 2.删除暂存区的文件

~~~apl
git rm --cached 文件名
~~~

![截屏2021-05-26 下午10.18.28](/Users/wking/Library/Application Support/typora-user-images/截屏2021-05-26 下午10.18.28.png)

这个就代表把暂存区的文件删除了，但是工作区文件还是存在，我们可以通过ls查看

---



### 3.将git仓库中指定的更新记录恢复，并且覆盖到工作区和暂存区

~~~apl
git rest --hard commitID
~~~

   git log 先查看提交的更新记录

<img src="/Users/wking/Library/Application Support/typora-user-images/截屏2021-05-26 下午10.35.58.png" alt="截屏2021-05-26 下午10.35.58" style="zoom:50%;" />

  然后找到你要恢复的文件id 就是commit后面一串

~~~apl
 git reset --hard bc58b8dcfcbe3098ef9c30b2b9d09e63d6904990
~~~

这样文件就恢复了,**我们在git log去查看提交记录时发现，只剩下我们刚恢复的文件，之后提交的都被删除了** 

<img src="/Users/wking/Library/Application Support/typora-user-images/截屏2021-05-26 下午10.45.25.png" alt="截屏2021-05-26 下午10.45.25" style="zoom:50%;" />

---

## Git分支

查看分支，命令

~~~assembly
git branch
~~~

<img src="/Users/wking/Library/Application Support/typora-user-images/截屏2021-05-27 上午2.37.35.png" alt="截屏2021-05-27 上午2.37.35" style="zoom:50%;" /> 这是第一次提交系统默认创建的主分支

创建分支

~~~apl
git branch 分支名
~~~

<img src="/Users/wking/Library/Application Support/typora-user-images/截屏2021-05-27 上午2.43.15.png" alt="截屏2021-05-27 上午2.43.15" style="zoom:50%;" />

切换分支

~~~apl
git checkout 分支名
~~~



<img src="/Users/wking/Library/Application Support/typora-user-images/截屏2021-05-27 上午2.46.27.png" alt="截屏2021-05-27 上午2.46.27" style="zoom:50%;" />

**在分支上提交文件时，一定要先提交到本地仓，不然在切换分支时这个分支会被带到其他分支**

分支合并

~~~apl
git merge 来源分支 合并分支
~~~

**注意 一定要先切换到主分支，在它的角度来合拼分支*,及时合拼了但是这个分支依然在**

<img src="/Users/wking/Library/Application Support/typora-user-images/截屏2021-05-27 上午3.06.59.png" alt="截屏2021-05-27 上午3.06.59" style="zoom:50%;" />

删除分支

~~~apl
git branch -d 删除分支名字
~~~

 <img src="/Users/wking/Library/Application Support/typora-user-images/截屏2021-05-27 上午3.09.30.png" alt="截屏2021-05-27 上午3.09.30" style="zoom:50%;" />

**注意，一般要删除分支要在合拼后，这是一种保护，防止误删，但是如果要来强的-d改成-D"就可以了**

---

## 暂时保存修改

在git中暂时储存分支上所有的改动，临时转向其他工作

储存的临时改动

~~~apl
git stash
~~~

![截屏2021-05-27 上午3.35.25](/Users/wking/Library/Application Support/typora-user-images/截屏2021-05-27 上午3.35.25.png)

取出来恢复

~~~apl
git stash pop
~~~



## 将本地的提交到线上仓库

这是提交到主分支

~~~assembly
git push https://github.com/King-W99/King.git master

~~~

<img src="/Users/wking/Library/Application Support/typora-user-images/截屏2021-05-27 上午4.20.48.png" alt="截屏2021-05-27 上午4.20.48" style="zoom:50%;" />

但是这个仓库地址太长太tm麻烦了，加别名

~~~
git remote add  别名  远端仓库地址
~~~

~~~apl
git remote add origin https://github.com/King-W99/King.git
~~~

在提交就变成

~~~apl
git push origin master
~~~



   再次简化 加上-u 下次提交就会记住仓库地址和分支

~~~apl
git push -u origin master
~~~

  ~~~apl
  git push        
  ~~~



  ## 远程仓库克隆到本地仓库

~~~apl
git clone 仓库地址
~~~

拉取远程仓库最新的版本

~~~apl
git pull 远程仓库地址
~~~



## SSH免登录

生成密钥

~~~apl
wking@WdeMacBook-Pro ~ % ssh-keygen -t rsa -C "2457808858@qq.com"
~~~

然后再电脑目录可以看到.ssh目录

~~~apl
id.rsa 公钥   放到githu服务器中
id.rsa.pub 私钥 放到自己电脑中
~~~



## git忽略清单

将不需要git管理的文件名字添加到此文件中，在执行git命令时就会忽略这些文件

git忽略清单名称 .git

