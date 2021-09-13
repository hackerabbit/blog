---
title: git基本操作
date: 2020-12-16
tags:
 - git
categories: 
 - git
---

#### 如何上传代码至github
- 本地区
- 暂存区
- 远程仓库
- git init 
    - 初始化git文件
- git add .
    - 将本地文件添加到暂存区
- git commit -m (提示)
    - 将暂存区文件推送到远程仓库
- git status
    - 查看当前代码的状态
- git log 
    - 查看代码日志
- git log --author="(查看单个人提交的代码纪录)"
- git config --global user.name (名字)
- git config --global user.email (邮箱)
- git config --global --list

##### 删除文件
- 手动邮件删除
- git rm (文件名)

##### 重命名文件
- 手动重命名文件
    1.右键修改文件名字
    2.git add ./
- 命令修改重命名文件
    1.git mv originName newName

##### 移动文件
- git mv 文件 文件夹

##### 查看文件信息
- git log --pretty=online 文件名
- git show (id)
- git log -p 文件名

##### 操作失误怎么还原(回滚)
- git checkout -- 文件名
- 还原当上次提交的状态

##### 撤销状态的追踪
-   当文件git add到暂存区时，需要使用撤销状态追踪，然后在执行回滚
- git reset HEAD 文件名

##### 版本回归
- git reset --hard HEAD^(一个^表示回退到上一个版本)
- git reset --hard id(使用git log获取指定的id，可以回到指定的版本)

##### 将某一文件回到指定版本
- git checkout (id) -- 指定文件名

- git tag 版本号 
- git tag -d 版本号

- 分支切换，删除分支时如何进行操作。
    - 方便多人协作开发
- 创建分支
    - git branch 分支名
- 查看分支
    - git branch
- 切换分支
    - git checkout 分支名
- 删除分支(正在使用的分支没办法删除)
    - git branch -d 分支名
    - 强行删除分支
        - git branch -D 分支名
- 创建并且切换分支
    - git checkout -b 分支名
- 合并分支
    - 切换到main分支
    - git merge 需要合并的分支
- 解决分支合并冲突
    - 产生条件
        - 当在不同分支修改同一地方的时候
    - git merge --abort(报错当前分支的代码)
    - 手动修改
- 查看不同人查看版本路线
    - git log --oneline 
    - git log --oneline --graph
- 不用人删除不想要的分支
    - <font color="red">确认该分支是否不需要了</font>
    - git push orgin --delete 远程分支名
- 不同人修改不同文件处理
    - 没有出现该问题
- 显示远程分支与本地分支的关系
    - git branch -av
- 拉去远程分支
    - git fetch
- github拓展
    - 安装chrome插件octotree
        - 作用提供一个项目树结构
    - Gitzip for github
        - 下载单个文件夹
    - Enhanced Github
        - 可以下载单个文件和显示单个文件的大小
- 解决github下载慢的问题
    - 最简单的搭梯子
    - 使用gitee转存，然后下载(个人比较推荐)