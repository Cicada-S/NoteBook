### Git 环境配置



### Git 基础

```
git init

git status

git add .

git commit -m 'first commit'

git remote add origin 仓库地址(https://github.com/)

git push -u origin main

// 克隆一个远程的仓库
git clone git@github.com:ngd-b/Git-Project.git
```





### Git 常用命令

```
// 添加到暂存区
git add 

// 提交到本地库
git commit -m

// 上传到远程仓库
git push 

// 查看状态
git status

// 修改文件
vim <file>

// 保存
WQ

// 查看版本信息
git reflog

// 查看版本详细信息
git log

// 查看文件
cat <file>

// 版本穿梭   5770506  版本号
git reset --hard 5770506
```



### Git基本理论

* Git 的工作就是创建和保存你项目的快照及与之后的快照进行对比。
* Git 常用的是以下 6 个命令：**clone**、**push**、**add** 、**commit**、**checkout**、**pull**

**说明：**

+ workspace：工作区
+ staging area：暂存区/缓存区
+ local repository：版本库或本地仓库
+ remote repository：远程仓库



### 创建本地仓库

1. 创建全新的仓库
```
$ git init
```

2. 克隆远程仓库
```
$ git clone [url] https://github.com/Cicada-S/supermall.git
```

3. 远程仓库路径查询

```
git remote -v

// 删除指定的远程
git remote rm origin
```



### Git 文件操作

**文件四种状态**

* Untracked: 未跟踪，此文件在文件夹中，但并没有加入到git库，通过  ==git add==  状态改为Staged.
* Unmodify: 文件已经入库，未修改，即版本库中的文件快照内容与文件夹中完全一致，这种类型的文件有两种去处，如果它被修改，而变为  ==Modified==  ，如果使用  ==git rm==  移除版本库，则成为  ==Untracked==  文件
* Modified: 文件已修改，仅仅是修改，并没有进行其他的操作，这个文件也有两个去处，通过  ==git add== 可进入暂存  ==staged==  状态，使用   ==git checkout==  则丢弃修改过，返回到  ==unmodify==  状态，这个  ==git checkout==  即从库中取出文件，覆盖当前修改！
* Staged: 暂存状态，执行  ==git commit==  则将修改同步到库中，这时库中的文件和本地文件又变为一致，文件为  ==Unmodify==  状态，执行==git reset HEAD filename==  取消暂存，文件状态为  ==Modified==   



**查看文件状态**

```
// 查看指定文件状态
git status [filename]

// 查看所有文件状态
git status 

// 添加所有文件到暂存区
git add .

// 提交暂存区中的内容到本地仓库  -m 提交信息
git commit -m "消息内容"
```



**忽略文件**

````
// 忽略所有 .txt 结尾的文件，这样的话上传就不会被选中！
*.txt

// 但 lib.txt 除外
!lib,txt

// 仅忽略项目根目录下的TODO文件，不包括其他目录temp
/temp

// 忽略build/目录下的所有文件
build/

// 会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
doc/*.txt
````



### 使用码云

1. 注册登录码云，完善个人信息

2. 设置本机绑定SSH公钥，实现免密登陆！

   ```\
   // 进入 C:\Users\Adminstrator\.ssh 目录
   // 生成公钥
   ssh-keygen
   ```

3. 将公钥信息 pubic key 添加到码云 账户中即可！

4. 使用码云创建一个自己的仓库！

5. github 国外，gitee 国内，gitlab 自己搭建



### git分支

* 常用命令

```
// 查看分支
git branch -v

// 创建分支 hot-fix(分支名)
git branch hot-fix

// 删除分支
git branch -d hot-fix

// 切换分支 
git checkout hot-fix

// 合并分支 合并分支要在主分支 进行合并
git merge hot-fix
```

### Git 分支

#### 新建分支

```
git checkout -b name // name 分支名称
```

#### 查看所有分支

```
git branch
```

#### 切换分支

```
git checkout master // master 分支名称
```

#### 合并分支

```
git merge login // login 分支名称 
注意：合并分支要在主分支 进行合并
```

 #### 将分支推送到云端

```
git push -u origin name // name 分支名称
```



### 提交指定文件

```
git status
git add 文件名
git stash -u -k  忽略其他文件
git commit -m ''
git pull 拉取合并
git push 推送到远程仓库
git stash pop 恢复之前忽略的文件
```

