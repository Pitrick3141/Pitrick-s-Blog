---
title: "Window下TensorFlow环境的配置(GPU)"
date: 2021-12-28
draft: false
description: "Windows系统下TensorFlow的安装及配置教程"
images: []
resources:
- name: "featured-image"
  src: "featured-image.png"

tags: ["python","tensorflow"]
categories: ["tutorials"]

lightgallery: true
---

Windows系统下TensorFlow的安装及配置教程
<!--more-->

## 1 介绍

TensorFlow是一个能方便的搭建神经网络实现深度学习或强化学习的第三方Python库。相信许多人对TensorFlow并不陌生，当在家用电脑上训练较大的数据集时，可能会消耗较长的时间。这时如果你的电脑有一个较好的显卡，使用GPU加速就不失为一个好方法。

*注：本文整合了几篇我摸索时借鉴的教程，仅供学习交流使用*

## 2 配置需求

### 2.1 我的电脑配置及系统版本

- Windows11 21H2
- Intel Core i7-10875H
- NVIDIA GeForce RTX 2060

### 2.2 TensorFlow官网提供的最新版(2.7.0)驱动需求(N卡)

{{< admonition warning "配置需求">}}
**下面列出的仅为运行的最低需求，详细请参考[官方网站](https://www.tensorflow.org/install/gpu?hl=zh-cn)**
{{< /admonition >}}

- [NVIDIA驱动程序](https://www.nvidia.cn/Download/index.aspx?lang=cn) >= 450.80.02
- [CUDA 11.2](https://developer.nvidia.com/cuda-11.2.0-download-archive)
- [cuDNN SDK 8.1.0](https://developer.nvidia.com/compute/machine-learning/cudnn/secure/8.1.0.77/11.2_20210127/cudnn-11.2-windows-x64-v8.1.0.77.zip)(**第一次下载需要注册及填写调查问卷**)

## 3 Python环境的配置(以Anaconda为例)

### 3.1 下载最新版[Anaconda](https://www.anaconda.com/products/individual)(以个人版为例)

### 3.2 安装Anaconda及配置环境变量(可选)：详见Segmentfault提供的[教程](https://segmentfault.com/a/1190000037752539)

### 3.3 新建一个虚拟环境(详细步骤见下)

![①在Anaconda主页面选择”Environments”](https://s4.ax1x.com/2021/12/29/T65XDS.png "3.3.1 在Anaconda主页面选择“Environments”")

![②点击“Create”按钮](https://s4.ax1x.com/2021/12/29/T65Ou8.png "3.3.2 点击“Create”按钮")

![③建立一个Python3.9.9的虚拟环境](https://s4.ax1x.com/2021/12/29/T6IUPA.png "3.3.3 建立一个Python3.9.9的虚拟环境")

### 3.4 打开Anaconda Prompt或Windows终端(**在已经配置好环境变量的情况下**)并输入如下指令(*注：”//”后为注释，解释当行指令意义，无需输入*)

```
conda activate 你的自定义环境名称 //选择你新创建的环境
conda install pip //安装pip第三方库管理工具(默认自带，但还是安装一下)
pip install tensorflow //安装最新版本tensorflow
```

**至此，Python及TensorFlow环境配置完成。**

***

## 4 CUDA与cuDNN的安装与配置

### 4.1 确认你的显卡支持的CUDA版本

![①打开NVIDIA控制面板，点击左下角的“系统信息”](https://s4.ax1x.com/2021/12/29/TgxJII.png "4.1.1 打开NVIDIA控制面板，点击左下角的“系统信息”")

![②在“系统信息”窗口中点击“组件”选项卡](https://s4.ax1x.com/2021/12/29/Tgx8Zd.png "4.1.2 在“系统信息”窗口中点击“组件”选项卡")

![③红框内即为支持的CUDA版本，可以安装低于或等于该版本号的CUDA](https://s4.ax1x.com/2021/12/29/TgxGdA.png "4.1.3 红框内即为支持的CUDA版本，可以安装低于或等于该版本号的CUDA")

### 4.2 在电脑上安装CUDA(以CUDA11.2为例)

#### 4.2.1 下载CUDA11.2[安装包](https://developer.nvidia.com/cuda-11.2.0-download-archive)

![①下载CUDA11.2安装包](https://s4.ax1x.com/2021/12/29/TgxzeH.png "如图，选择适合你电脑操作系统，架构，版本的安装包并点击“Download”即可下载")

#### 4.2.2 下载完成后，以管理员身份运行并安装，所有选项都默认即可

### 4.3 在安装完CUDA的基础上安装cuDNN(以cuDNN8.1为例)

#### 4.3.1 打开cuDNN[下载页面](https://developer.nvidia.com/rdp/cudnn-download)，完成调查问卷并勾选同意协议，选择合适版本下载

![①打开cuDNN下载页面，完成调查问卷并勾选同意协议，选择合适版本下载](https://s4.ax1x.com/2021/12/29/Tgz51f.png "勾选同意使用守则")

![①打开cuDNN下载页面，完成调查问卷并勾选同意协议，选择合适版本下载](https://s4.ax1x.com/2021/12/29/T2SMHH.png "选择”Archived cuDNN Releases”")

![①打开cuDNN下载页面，完成调查问卷并勾选同意协议，选择合适版本下载](https://s4.ax1x.com/2021/12/29/T2S1UA.png "选择合适的版本(以8.1.0为例)")

![①打开cuDNN下载页面，完成调查问卷并勾选同意协议，选择合适版本下载](https://s4.ax1x.com/2021/12/29/T2SlEd.png "选择适合自己操作系统的版本(以Windows为例)")

#### 4.3.2 下载完成后，打开下载的安装包，将内容解压至CUDA安装目录对应文件夹

{{< admonition tip "小贴士" >}}
CUDA默认安装目录(以11.2为例):C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.2
{{< /admonition >}}

![②下载完成后，打开下载的安装包，将内容解压至CUDA安装目录对应文件夹](https://s4.ax1x.com/2021/12/29/T2pbYn.png "cuDNN内部文件结构")

![②下载完成后，打开下载的安装包，将内容解压至CUDA安装目录对应文件夹](https://s4.ax1x.com/2021/12/29/T2pqWq.png "将对应文件夹中文件解压至对应文件夹")

**至此，CUDA与cuDNN环境配置完毕。**