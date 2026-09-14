---
date: '2026-07-30T12:00:00+09:00'
title: '基于CF的优选域名搭建(其一：使用华为云)'
categories:
  - 
tags:
  - 教程
---
{{< heatMapCard levelStandard="200,500,2000" >}}
### 提前准备
1. Cloudflare账号 x1

2. 华为云国际版账号 x1

3. 域名 x1，注意不能是 xxx.cc.cd、xxx.ddns.ge等复合后缀产生的域名后缀
## 步骤
1. 在 Cloudflare 内新建一个worker，名称任意，**不能绑定自定义域**~~绑定自己域名 `cf.example.com`~~

2. 点击【编辑代码】，将以下代码粘贴进去，点击【部署】，访问显示 OK 即完成

```worker.js
骗你的，worker里不用加内容
但如果想让域名被访问时显示内容，则根据需要编写即可
```

3. 在华为云国际版内添加该域名，并在 Cloudflare 内手动添加相关的 NS 记录

4. 先使用 `nslookup` 命令检查域名是否显示你的 worker 地址，并检查你的网络是否使用了Cloudflare的服务，如 DOT、DOH、1.1.1.1等，将其关闭或修改为国内相关内容，若不检查将影响后续值

{{< details summary="为什么要改这些值？" >}}
若不修改，通过`nslookup`显示出的是域名解析到国外的记录，延迟偏高
{{< /details >}}

5. 使用 AI （本地可使用 opencode 等） 查找别人现成的优选域名或优选IP，不想找的话可前往[次元星域优选域名](https://cf.107211.xyz/)复制，挑选延迟低，dns 快且干净的优选域名

6. 按下表参考样式填写

| 域名 | 记录类型 | 线路类型 | TTL | 记录值 | 备注 |
| :---: | :---: | :---: | :---: | :---: | :---: |
| cf.example.com | CNAME | 全网默认 | 300 | 你的worker地址 | / |
| cf.example.com | CNAME | 中国大陆 | 300 | 你找的优选域名的域名上游 | 使用 `nslookup`查找 |
| *.cf.example.com | CNAME | 全网默认 | 300 | 同上 | 同上 |

↑上表为新方案

下表为旧方案↓

| 域名 | 记录类型 | 线路类型 | TTL | 记录值 | 备注 |
| :---: | :---: | :---: | :---: | :---: | :---: |
| cf.example.com | CNAME | 全网默认 | 300 | 你的worker地址 | / |
| cf.example.com | CNAME | 中国大陆 | 300 | 你找的优选域名 | 若找的是优选IP，此时【记录类型】为A，记录值为优选IP |
| *.cf.example.com | CNAME | 全网默认 | 300 | 你找的优选域名 | 同上 |

{{< details summary="什么是域名上游？" >}}
通过`nslookup`显示，以saas.sin.fan为例
使用命令 `nslookup saas.sin.fan`后，会显示以下内容：
非权威应答:
名称:    singgcdn.singgnetworkcdn.com
Addresses:  162.159.135.234
          162.159.130.234
Aliases:  saas.sin.fan
那么上方记录值填写 `singgcdn.singgnetworkcdn.com`
{{< /details >}}

7. 稍等一两分钟，再次使用 `nslookup` 命令检查域名，若能顺利显示配置的内容则进行下一步

8. 使用 `ping xx.example.com` 测试延迟，或使用 itdog 等测速网站 ping 测速和 dns 测速，若 ping 值小于70，再进行下一步

9. 使用 AI （本地可使用 opencode 等）测试域名是否可作为优选域名使用，让其全面测试并给出结论，担心结论不准确可使用多个AI测试，这种测试一般都很准确的

10. 若结论为“可作为优选域名使用”或其他类似语句，可视为自建优选域名完成；否则，返回检查