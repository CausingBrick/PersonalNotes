# ubuntu 安装为知笔记

## 一. 问题背景

wiz是一款跨平台的笔记软件,在安装于Ubuntu comsic版本上遇到问题

## 二. 过程

1. 正常从官网下载的linux安装文件appimage, 给予执行权限以后依旧安装不上.
2. 源码编译,通过官方教程编译源码,qt装完以后编译失败(可能是qt未下载完全)
3. 网上添加的源不一样,通过查找找到两个源,其中之一失效

## 三. 解决方案

>sudo add-apt-repository ppa:wiznote-team  
sudo apt update  
sudo apt install wiznote

*在上面的源里,若更新失败,就把版本号改为xeninl.*

+ 给出源url与版本:

  ><http://ppa.launchpad.net/wiznote-team/ppa/ubuntu>   xenial  main
