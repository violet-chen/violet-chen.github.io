---
title: 从零开始安装ComfyUI
tags: ComfyUI
categories: AI
abbrlink: 13f6974d
date: 2024-06-18 17:16:00
---
# 大概过程总结
确保拥有git -> 拉取comfyui的github仓库 -> 使用conda配置comfyui的对应环境 -> 使用.bat文件来方便运行启动comfyui 
# 安装git
git官方网站:https://www.git-scm.com/
# 拉取comfyui的github仓库
https://github.com/comfyanonymous/ComfyUI
在你要安装comfyui的盘中右键打开git bash
![alt text](image.png)
在界面中输入:
```bash
git clone https://github.com/comfyanonymous/ComfyUI.git
```
如果是第一次使用git,可能会有注册github账号,配置账号,下载速度慢的问题.这些问题都可以通过谷歌百度得到详细的问题解决过程,这里不再赘述.
# 使用conda配置python环境
## 安装conda
通过使用conda可以方便地进行python环境的管理,常见的对应软件有,anaconda,miniconda,miniforge,这三个更推荐miniconda,如果公司不让用anaconda和miniconda的话可以使用miniforge代替.
请谷歌搜索自行下载与安装,下载和安装conda网上有很多.
**需要强调的是安装完conda以后需要手动配置环境变量,不然没办法使用conda命令**
在Path变量中新建添加类似于这两个的路径
![alt text](image-1.png)
**添加完环境变量以后需要重新开一个终端**
## 通过conda配置comfyui的python环境
在comfyui的文件夹上输入cmd进入对应路径的终端
![alt text](image-2.png)
根据终端中显示的提示依次输入命令回车.命令的作用是:创建comfyui的基础环境,激活这个环境
```bash
conda create -n comfyuiBase python=3.10
conda activate comfyuiBase
```
## 在comfyuiBase环境中安装pytorch
在上一步中,已经通过conda创建了一个comfyuiBase的环境并且已经激活.
接下来为需要在comfyuiBase环境中安装pytorch.
如果你的电脑是n卡的话,可以在终端中输入命令查看自己的显卡支持的cuda版本.
```bash
nvidia-smi
```
![alt text](image-4.png)

接下来你需要去谷歌搜索cuda去进行cuda的安装

安装完cuda之后安装pytorch
进入pytorch的网站
https://pytorch.org/get-started/locally/
根据自己的所支持的cuda版本(你的cuda版本需要大于界面中选择的cuda版本),使用对应的命令进行安装.
![alt text](image-3.png)
在comfyuiBase环境下安装完pytorch后,安装comfyui的依赖环境,并通过python main.py来打开comfyui进行环境测试
```bash
pip install -r requirements.txt
python main.py --auto-launch
```

## 基于配置好的comfyuiBase环境,创建属于自己的comfyui环境(可不做)
经过前面的环境配置以后你就拥有了运行comfyui所需要的最基础的环境.
接下来你可以保留这个最基础的comfyui环境,创建一个自己平时使用的comfyui环境.
这样环境随便搞,后面搞坏了也有一个基础的可以用的环境.
在终端中输入命令,基于comfyuiBase环境创建一个新的环境,我这里命名为comfyui.
```bash
conda create comfyui --clone comfyuiBase
```

# 使用.bat文件来方便运行启动comfyui
在comfyui文件夹中新建一个txt文件,然后输入类似于下面的内容
第二行activate comfyui是激活你的comfyui环境(因为我创建的环境名字是comfyui所以填comfyui)
第三行C:\ComfyUI对应你的comfyui的文件夹路径
```bash
@echo off
call activate comfyui
cd C:\ComfyUI
python main.py --auto-launch
pause
```
填好以后保存txt文件,改后缀名为.bat,这样以后都可以通过这个.bat文件直接激活comfyui环境并启动comfyui了.
