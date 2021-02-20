# git–工作区、暂存区、版本库、远程仓库

## 一、概念

### 1、四个工作区域

1. **Workspace:** 工作区，就是你平时存放项目代码的地方

2. **Index / Stage:** 暂存区，用于临时存放你的改动，事实上它只是一个文件，保存即将提交到文件列表信息

3. **Repository:** 仓库区（或版本库），就是安全存放数据的位置，这里面有你提交到所有版本的数据。其中HEAD指向最新放入仓库的版本

4. **Remote:** 远程仓库，托管代码的服务器，可以简单的认为是你项目组中的一台电脑用于远程数据交换

   

![4workdir](https://github.com/yandong2015/gitstudy/blob/main/image/4workdir.png)

### 2、工作流程

git的工作流程一般是这样的：

1.  在工作目录中添加、修改文件；
2. 将需要进行版本管理的文件放入暂存区域；
3. 将暂存区域的文件提交到git仓库。
4. 因此，git管理的文件有三种状态：已修改（modified）,已暂存（staged）,已提交(committed)

### 3、文件的四种状态

1. **Untracked:**  未跟踪, 此文件在文件夹中, 但并没有加入到git库, 不参与版本控制. 通过git add 状态变为Staged.
2.  **Unmodify:**  文件已经入库, 未修改, 即版本库中的文件快照内容与文件夹中完全一致. 这种类型的文件有两种去处, 如果它被修改, 而变为Modified.如果使用git rm移出版本库, 则成为Untracked文件

    3.  **Modified:** 文件已修改, 仅仅是修改, 并没有进行其他的操作. 这个文件也有两个去处, 通过git add可进      暂存staged状态, 使用git checkout 则丢弃修改过,返回到unmodify状态, 这个git checkout即从库中取出文件, 覆盖当前修改

4.  **Staged:** 暂存状态. 执行git commit则将修改同步到库中, 这时库中的文件和本地文件又变为一致, 文件为Unmodify状态. 执行git reset HEAD filename取消暂存,文件状态为Modified

​        

下面的图很好的解释了这四种状态的转变：![statetransfer](statetransfer.png)

* 新建文件--->Untracked
* 使用add命令将新建的文件加入到暂存区--->Staged
* 使用commit命令将暂存区的文件提交到本地仓库--->Unmodified
* 如果对Unmodified状态的文件进行修改---> modified
* 如果对Unmodified状态的文件进行remove操作--->Untracked

## 二、四个区域常用命令

### 1、新建代码库

~~~shell
# 在当前目录新建一个Git代码库
 git init
# 新建一个目录，将其初始化为Git代码库
git init [project-name]
# 下载一个项目和它的整个代码历史
git clone [url]
~~~

### 2 、查看文件状态

~~~shell
#查看指定文件状态
git status [filename]
#查看所有文件状态
git status
~~~

### 3、工作区<-->暂存区

~~~shell
# 添加指定文件到暂存区
git add [file1] [file2] ...
# 添加指定目录到暂存区，包括子目录
git add [dir]
# 添加当前目录的所有文件到暂存区
git add .
#当我们需要删除暂存区或分支上的文件, 同时工作区也不需要这个文件了, 可以使用（⚠️）
git rm file_path
#当我们需要删除暂存区或分支上的文件, 但本地又需要使用, 这个时候直接push那边这个文件就没有，如果push之前重新add那么还是会有。
git rm --cached file_path
#直接加文件名   从暂存区将文件恢复到工作区，如果工作区已经有该文件，则会选择覆盖
#加了【分支名】 +文件名  则表示从分支名为所写的分支名中拉取文件 并覆盖工作区里的文件
git checkout
~~~

