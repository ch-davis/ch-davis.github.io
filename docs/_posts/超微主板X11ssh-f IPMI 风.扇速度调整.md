---
# 文章标题
title: 超微主板X11ssh-f IPMI 风扇速度调整
# 设置写作时间
date: 2024-11-28
# 一个页面可以有多个分类
category:
  - 使用指南
# 一个页面可以有多个标签
tag:
 - 使用指南
# 此页面会在文章列表置顶
sticky: true
# 此页面会出现在文章收藏中
star: true
# 侧边栏的顺序
# 数字越小越靠前，支持非整数和负数，比如 -10 < -9.5 < 3.2, order 为 -10 的文章会最靠上。
# 个人偏好将非干货或随想短文的 order 设置在 -0.01 到 -0.99，将干货类长文的 order 设置在 -1 到负无穷。每次新增文章都会在上一篇的基础上递减 order 值。
order: -1
bgImage: https://img.newzone.top/home-bg-1.jpg
---

## 通过IPMI命令行设置风扇模式
可以通过IPMI命令行工具来设置这些模式。以下是设置命令的通用格式
```shell
ipmitool -H IPMI_IP -U USERNAME -P PASSWORD raw 0x30 0x45 0x01 MODE_HEX
```
其中，MODE_HEX 为相应模式的十六进制代码：
 > [!note]
>| 模式 | 十六进制代码 |
>|:-----|---------------|
>|    Standard|       0x00| 
>|     Full（全速模式） |        0x01       |
>|     Optimal（最优转速模式）|          0x02      |
>|     Heavy IO（高负载IO模式）|        0x03       |


要将风扇模式设置为全速模式，您可以使用以下命令：
```
ipmitool -H 192.168.31.252 -U ADMIN -P ADMIN raw 0x30 0x45 0x01 0x01
```
> 请注意，IP地址、用户名和密码应替换为你的IPMI设置

## 风扇转速命令说明
```shell
ipmitool -H 192.168.31.252 -U ADMIN -P ADMIN raw 0x30 0x70 0x66 0x01 0x00 0x24
```
其中最后一组 `0x24`代表速度比，最低为`0x00`
倒数第二位`0x00`代表风扇 FAN1,......等
> 请注意，IP地址、用户名和密码应替换为你的IPMI设置
- 关于上面命令的说明
    - U 和-P 分别指定 IPMI 的用户名和密码
   - 0x24 是 16 进制的，0x24 代表风扇转速设置成 36%
 以上

