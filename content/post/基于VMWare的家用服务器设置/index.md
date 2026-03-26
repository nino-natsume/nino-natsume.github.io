---
date: '2026-03-01T11:00:00+09:00'
title: '基于VMWare的家用服务器设置'
categories:
  - 次元星域
tags:
  - 次元星域
  - Hugo
  - 教程
---
{{< heatMapCard levelStandard="200,500,5000" >}}
## 前言
有些地区的运营商不会给用户开放公网ip，如果有也可能是动态公网，使用起来特别不友好

如果用户有建站的需求，那么他大概率会想到在服务器商处购买服务器和域名，在国内的服务器还需要备案等，非常麻烦对吧？

但是，如果我说现在有种方案，只要你有一部可上网的电脑、一个国外域名即可无需服务器完成网站外网访问，那么，你，会选择尝试吗？

本方案类似于 Nas 搭建服务器，部分操作几乎一致
### 必备准备
在完成本项前请确保你已拥有以下东西：

1. 一部可正常上网的电脑

2. 一个 Cloudflare 账号

3. 已在 Cloudflare 解析的 **国外**域名

4. 【非必须】一个空间足够大的外接硬盘，仅为有多余硬盘的用户操作
## 前期操作
### 创建服务器
1. 自行下载和安装VMWare 25H2，并创建典型虚拟机，配置可按下方表格设置

表格的每行代表一个步骤，含 _&_ 的表示该步骤内有选填项，需按实际修改或操作

| 步骤 | 设置 |
| :---: | :---: |
| install from: | I will install the operating system later. |
| Guest operating system & Version | Linux & Debian 13 x64位|
| Virtual machine name & Location | Debian 13 & D:\Desktop\VMWare |
| 最大磁盘大小（GB） | 20 & 将虚拟磁盘拆分成多个文件|
| 已准备好创建虚拟机 | 完成 |

设置虚拟机，点击编辑虚拟机设置：

| 设备 | 摘要 |
| :---: | :---: |
| 内存 | 4GB（以物理机配置灵活调节） |
| 处理器 | 4（以物理机配置灵活调节）|
| 硬盘 | 20GB（建议40GB，以物理机配置灵活调节，若使用外接硬盘，此项应删除，创建好系统后再添加） |
| CD/DVD(SATA) | 选择系统镜像文件所在路径 |
| 网络适配器 | NAT（或桥接，视需求决定） |
| USB控制器 | USB 3.2 & 显示所有 USB 输入设备 |
| 声卡 | 此项删除 |

{{< details summary="补充说明" >}}

1. VMWare可视需求自行选择是否使用汉化，当前汉化包翻译可能不完全，但足够日常使用了

2. 若使用外接硬盘，此项必做，请先删除【设置】中【硬盘】项，退出VMWare，使用管理员权限打开，进入设置界面，选择硬盘，设置内会显示 PhysicalDriver0 或 PhysicalDriver1 等，找到对应你外接硬盘的硬盘大小的物理磁盘后点击保存，再按上表配置其他设置

3. 系统镜像文件可在[此处](https://pan.107211.xyz/s/aycw)获取

4. 【网络适配器】栏的选择，若想让虚拟机独占一个 ip 选择桥接，否则选择 NAT，配置桥接的方法将在下方讲解，可在下方查看
{{< /details >}}

2. 保存设置后，正式进入系统安装界面，本过程预计耗时30min，需随时查看安装进度以进入下一安装步骤

3. 根据以下配置完成系统安装

| 步骤 | 设置 |
| :---: | :---: |
| 启动界面 | Graphical install（若使用 install，即命令行安装，操作与下一致） |
| 选择语言、国家、时区 | Chinese & China & China |
| 主机名 & 域名 & 密码 | 任意，如ciallo & 留空 & 自行输入 |
| 普通用户全名 & 登录用户名 & 密码 | 任意 & 任意 & 任意 |
| 磁盘选择 & 选择磁盘 | 使用整个磁盘（Guided - use entire disk） & SCSI? （根据自己设的大小选择） |
| 选择分区模式 & 完成并保存分区 | 所有目录都在根目录 & 完成分区 & 将改动应用至磁盘 |
| 可选项 | **不**扫描额外介质 & 启用网络镜像？（此处选 **是** & ustc.edu.cn）& **不**统计使用情况 |
| 选择安装的软件 **【此项必须一致，不然后续使用会有影响】** | Debian desktop environment & web server & SSH server & standard system utilities |
| 是否安装GRUB引导器至磁盘？ | 是 & /dev/sda |
| 等待重启 | 继续 |

4. 待重启后，使用普通用户的密码登录后，即可成功进入系统
 
### 服务器配置
打开系统终端（VMWare的，不是你物理机的），选择安装 **宝塔面板**或 **1panel**管理面板，这里以 1panel 为例

1. 打开终端后，输入 `su` ，输入管理员密码进入root模式，再输入以下代码完成初始环境和面板安装，1panel按自行喜好设置

```
sudo apt update
sudo apt-get install -y curl
bash -c "$(curl -sSL https://resource.fit2cloud.com/1panel/package/v2/quick_start.sh)"
```

{{< details summary="桥接模式设置（仅虚拟机设置了桥接时配置）" >}}
1. 关闭 VMWare，以管理员权限启动，点击菜单的【编辑】 - 【虚拟网络编辑器】，点击右下角的【变更设置】，修改VMnet0 的网卡为你自己 **实际在用的网卡**，点击保存，再启动虚拟机

2. 进入管理面板后，点击【终端】，输入 `ip address`，查看第二个设备的设备名，记住它

3. 点击【系统】 - 【文件】，打开 `/etc/network/interfaces` 文件，在文件内添加以下代码后，保存

```
auto [你的第二个设备名，要删外面括号]
iface [你的第二个设备名，要删外面括号] inet static
address 192.168.x.y                        # 输入你要给设备的ip，需确保不会与同网段ip冲突      
netmask 255.255.255.0
gateway 192.168.x.1                        # 输入设备网关，x是你上面填的值
```

4. 打开 `/etc/resolv.conf` 文件，输入以下内容并保存

```
nameserver 114.114.115.115
nameserver 8.8.8.8
nameserver 8.8.4.4
```

5. 打开【终端】，再次输入 `ip address`，查看设备是否为你给设备配置的ip，若是则完成桥接模式的配置，否则返回去检查
{{< /details >}}

2. 任意在应用商店安装一个应用，注意记得勾选 **端口外部访问**，若可通过 `内网ip:端口`的方式访问则基本服务正常
## Cloudflare的内网穿透设置
1. 打开Cloudflare，点击侧边栏【保护和连接】 - 【联网】 - 【Tunnels】，创建隧道，名字任意，点击【取消】

2. 点击刚创建的隧道，在【副本】选择系统（若使用本教程镜像应选择 Debian - arm64），复制最下面的代码至桌面的某个文件内备用，下方为参考示例

```隧道_例.md
cloudflared tunnel run --token eyJhIjoiMWM4YjY2ZmVlOWRkMzljMzE4OTg3MjZjZmY0NWFmMDgiLCJ0IjoiNDMyZDNk00QtNjc5NS00MmE5LWJiN2ItNDZjMGFhZjNkZjM2IiwicyI6Ik9HWTJNbVl6TmpRdFlUWTBOaTAwTlRJM0xUaGtZMkl0WlRjME9UWm1OV1kwWkRZdyJ9
```

3. 在虚拟机的期望文件夹内创建一个文件 docker-compose.yml ，输入以下代码并保存

```
version: '3.3'
services:
  cloudflared:
    image: cloudflare/cloudflared:latest
    container_name: cloudflared
    restart: unless-stopped
    command: tunnel run
    environment:
      - TUNNEL_TOKEN=eyJhxxxxxxxxxxxxxxxxxxxxdyJ9  # 提供 Token

```

4. 在当前文件夹的终端输入 `sudo docker compose up -d` 启动服务，返回Cloudflare，若状态为 健康，则隧道搭建完成

5. 隧道用法：点击【路由】 - 【添加路由】 - 【已发布的应用程序】，按照需求输入和选择域名，可参考下方示例填写

| 对应项 | 参考值 |
| :---: | :---: |
| 子域（可选） | anime |
| 域 | ciallo.cc |
| 路径（可选） | 留空 |
| 服务URL | http://192.168.91.78:721 |

6. 等待自动添加好CNAME记录后，访问域名，正常显示网页即成功