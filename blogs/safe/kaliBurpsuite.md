---
title: kali安装burpsuite Pro1.7.31
date: 2020-11-20
tags:
 - safe
categories: 
 - safe
---
### kali安装burpsuite Pro1.7.31
**没有找到新版的,所以将就着用**
**filename** 指的是文件夹的名字
1. 安装java
    - 建议版本1.8.0_181、1.8.0_191、1.8.0_201(版本很重要,有的版本启动不了,这里推荐的是oracle的版本)
2. 下载
    - [百度链接](https://pan.baidu.com/s/15VeuAwrzOqoDXLrSvuvPag) 密码:s5rx
3. 安装
    - 解压
        - tar -xzvf filename 
    - 移动(建议移动到opt目录)    这是主机给用户额外安装软件所摆放的目录
        - mv filename /opt
        - cd /opt/filename
    - 设置环境变量
        - vim ~/.bashrc
        - 在文件的最下面插入
            - #install JAVA JDK
            - export JAVA_HOME=/opt/filename
            - export CLASSPATH=.:${JAVA_HOME}/lib
            - export PATH=${JAVA_HOME}/bin:$PATH
        - 刷新环境变量
            - sudo  source ~/.bashrc
4. 安装jdk并且注册
    - 执行：
        - update-alternatives --install /usr/bin/java java /opt/jdk1.8.0_191/bin/java 1
        - update-alternatives --install /usr/bin/javac javac /opt/jdk1.8.0_191/bin/javac 1
        - update-alternatives --set java /opt/jdk1.8.0_191/bin/java
        - update-alternatives --set javac /opt/jdk1.8.0_191/bin/javac
    - 查看结果：
        - update-alternatives --config java
        - update-alternatives --config javac

5. 测试是否安装和配置成功
    - java --version
    - 成功显示文件的信息就成功了

6. 下载burpsuite1.7.31
    - [网盘链接](https://pan.baidu.com/s/11eM8aemNgW4Dr9mmxsuaew)
    - 密码:sq9u

7. 使用
    - 解压
        - 因为是zip文件,使用unzip命令解压
    - 新建启动脚本
        - sudo vim burpsuite.sh
        - 输入java -jar filename
        - 给权限 sudo chmod u+x burpsuite
        - ./burpsuite.sh
8.注册
    - 点击run
    - 复制License的激活码到Enter  license key里面 点击next  
    - 点击Manual activation 
    - 在Manual  activation窗口中 点击Copy request 复制内容到 Activation Request中
    - 复制Activation Response中的内容
    - 复制粘贴 Activation Response 里面的激活码到 Manual  activation 中的 Paste Response 点击next

### 完成
转载于:https://www.cnblogs.com/forforever/p/12976752.html
