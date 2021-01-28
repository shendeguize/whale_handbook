# Win10下C++/Python深度学习视觉环境配置指南

## 目录
- [Win10下C++/Python深度学习视觉环境配置指南](#win10下cpython深度学习视觉环境配置指南)
  - [目录](#目录)
  - [前言](#前言)
    - [pros & cons](#pros--cons)
    - [目标](#目标)
  - [0. 系统安装](#0-系统安装)
  - [1. Visual Studio](#1-visual-studio)
  - [2. Cuda](#2-cuda)
  - [3. Anaconda3](#3-anaconda3)
    - [3.1. PowerShell中conda支持](#31-powershell中conda支持)
    - [3.2. conda换源](#32-conda换源)
    - [3.3. pip换源](#33-pip换源)
  - [4. 工具及配置](#4-工具及配置)
    - [4.1. Git for Windows(实际主要为了bash)](#41-git-for-windows实际主要为了bash)
    - [4.2. VS Code](#42-vs-code)
    - [4.3. Github desktop](#43-github-desktop)
    - [4.4. 7zip](#44-7zip)
    - [4.5. Snipaste](#45-snipaste)
    - [4.6. PyCharm](#46-pycharm)
  - [5. Python环境配置&Trouble shooting](#5-python环境配置trouble-shooting)
    - [5.0. conda虚拟环境](#50-conda虚拟环境)
    - [5.1. pip](#51-pip)
    - [5.2. 一些特殊包](#52-一些特殊包)
    - [5.3. 路径](#53-路径)
    - [5.4. 环境迁移(待完善)](#54-环境迁移待完善)
      - [5.4.1. requirements+/conda yaml/spec list(待完善)](#541-requirementsconda-yamlspec-list待完善)
      - [5.4.2 conda pack(待完善)](#542-conda-pack待完善)
  - [6. C++环境(待完善)](#6-c环境待完善)
    - [6.1. Boost(待完善)](#61-boost待完善)
    - [6.2. OpenCV-C++(待完善)](#62-opencv-c待完善)
  - [7. Trouble Shooting](#7-trouble-shooting)
    - [7.1. pip常见错误](#71-pip常见错误)
    - [7.2. conda常见错误](#72-conda常见错误)
    - [7.3. 依赖/模型下载问题](#73-依赖模型下载问题)
      - [7.3.1. 判别是否在集群](#731-判别是否在集群)
      - [7.3.2. index server](#732-index-server)
  - [8. TBD](#8-tbd)

## 前言
### pros & cons
1. pro: 场景,工业视觉很多场景客户就是要求在Windows平台,win10甚至win7等环境下.So,不得不用Windows.
2. pro: C++/C#开发在win平台下用visual studio很方便
3. con: Python在win平台下有很多限制(包稍少一丢丢,pytorch的DataLoader有bug等)
4. pro/con: 环境配置各有优劣

### 目标
1. C++/C#开发环境
2. Python深度学习开发环境(conda,cuda)
3. 更多利用Win平台工具,并能够用一些工具/技巧来达到Linux的方便性(例如powershell)

## 0. 系统安装
就不太多说了,下面几点注意就可以
1. 安装专业版(不建议安装服务器版)
2. 更新驱动可以用驱动精灵,但是记得卸掉,另外别安360老流氓
3. 建议分区C(系统),D(软件),F(文件),然后尽量养成习惯别啥玩意都丢桌面,linux也得分配挂载不是
4. 序列号不行淘宝买一个,十来块,不贵,然后乱七八糟的系统更新根据情况决定要不要关闭自动更新
5. 养成习惯,涉及编程项目的目录不要有中文和特殊字符.

## 1. Visual Studio
第一步是要先安装vs,我习惯安2019,然后正常安在C盘什么的就行,等待时间比较长,安装勾选需要的功能即可,c++,c#之类的.主要是务必记得先安装vs就行.

## 2. Cuda
第二步才是安装cuda和cudnn.  
[cuda archive](https://developer.nvidia.com/cuda-toolkit-archive).  
[cudnn](https://developer.nvidia.com/cudnn-download-survey).需要登录账号,微信就可以扫码登录.下载对应版本即可.

无论是Windows还是Linux下,cuda都可以安装多个版本,通过环境变量配置来控制.不过对于一些特定版本(老一点版本的TensorFlow等)的深度学习库,可能对于特定的cuda版本有依赖.

## 3. Anaconda3
[Anaconda3官网](https://www.anaconda.com/products/individual)页面最下方下载64位版本即可.

安装中需要注意:
1. 勾选为所有账户/管理员账户安装
2. 建议安装在D盘,因为每次建立新环境等都会在Anaconda的安装目录下的env文件夹下建立,硬盘空间需求不小.

### 3.1. PowerShell中conda支持
1. 右键开始菜单图标,选择**PowerShell(管理员)**,运行
2. 输入`Set-ExecutionPolicy RemoteSigned`
3. 同意选项后,输入`conda init powershell`
4. 右键开始菜单图标,选择powershell,运行启动后,应该发现命令行最前面包含了一个`(base)`的虚拟环境标识.

### 3.2. conda换源
1. powershell中执行`conda config --set show_channel_urls yes`
2. 在用户目录下(以我自己为例`C:\Users\50391`)修改`.condarc`文件
3. 内容复制自[清华源Anaconda](https://mirrors.tuna.tsinghua.edu.cn/help/anaconda/)
4. 保存后,powershell中执行`conda clean -i`

### 3.3. pip换源
1. powershell中执行`pip install -i https://pypi.tuna.tsinghua.edu.cn/simple pip -U --user`
2. powershell中执行`pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple`

## 4. 工具及配置

### 4.1. Git for Windows(实际主要为了bash)
1. 下载[Git for Windows](https://gitforwindows.org/)
2. 运行,全都默认安装就行了.
3. 在开始菜单里输入`环境变量`,选择`编辑系统环境变量`,选择`环境变量`
4. 在`系统变量`中双击`Path`,点`新建`,点击`浏览`
5. 选择`C:\Program Files\Git\bin`,或者对应安装Git目录的bin目录.
6. 保存即可,在新的powershell中就可以使用bash命令了

### 4.2. VS Code
[VS Code](https://code.visualstudio.com/download)  
1. 中文设置https://blog.csdn.net/qq_30068487/article/details/82589347
2. 如果选择了加入环境变量中,那么在powershell里就可以类似于linux下的方式`code xxx.txt`进行操作了.
3. 为啥不用Notepad++(政治原因不喜欢)
4. Markdown All in One插件,非常好用(加目录)

### 4.3. Github desktop
[Github desktop](https://desktop.github.com/)  
非常好用的Git管理可视化工具.

### 4.4. 7zip
[7zip](https://sparanoid.com/lab/7z/)  
干净清爽,解压在右键菜单里

### 4.5. Snipaste
[Snipaste](https://zh.snipaste.com/)  
一个很好用的截图工具,在设置里可以设定快捷键,是否有辅助线,编辑功能也比较完善,安利.

### 4.6. PyCharm
[PyCharm](https://www.jetbrains.com/pycharm/download/)  
非常好用的Python开发工具,建议支持正版,一年八九十刀.

## 5. Python环境配置&Trouble shooting

### 5.0. conda虚拟环境
1. `conda create -n YOUR_ENV_NAME python==3.6.10`  
    python版本可以在这个时候对于不同环境更改,建议使用3.6以上
2. `conda activate YOUR_ENV_NAME`  
    启动虚拟环境
3. `conda deactivate`
    退出虚拟环境
4. `conda info --envs`  
    列出环境列表

### 5.1. pip
参见7.1

### 5.2. 一些特殊包
1. pycocotools
    [pycocotools-windows](https://github.com/maycuatroi/pycocotools-window)
2. 一些涉及编译的(比如mmcv的某些旧版本),需要使用msvc的  
    在`XXX\Anaconda3\envs\YOUR_ENV_NAME\Lib\distutils`下,新建`distutils.cfg`,内容如下
    ```
    [build]
    compiler=msvc
    ```

### 5.3. 路径
1. 不要使用相对路径!
2. 路径都使用形如`r""`的raw字符串
3. 不要有中文,不要有特殊字符,不要有空格

### 5.4. 环境迁移(待完善)

#### 5.4.1. requirements+/conda yaml/spec list(待完善)
可以导出requirements.txt或环境配置yaml或者spec list,再进行恢复

pros:
1. 轻量级

cons:
1. 不适用于依赖复杂的情况(对于TensorFlow/PyTorch等,有时系统环境变量也会有干扰)
2. 可能不适用于有私有包或者有编译迁移到不同平台(不同系统/不同硬件/不同驱动)的情况

#### 5.4.2 conda pack(待完善)
可以将conda环境打包成二进制文件.

pros:
1. 适用于无网络或网络受限或有私有包的情况

cons:
1. 需要相同平台环境才能迁移

## 6. C++环境(待完善)
c++的开发过程往往是有很多外部依赖库,我的习惯是放在`D:\lib`下,然后再VS里用配置表来导入,而不是注册环境变量.

### 6.1. Boost(待完善)
[Boost](https://www.boost.org/)  
万能的库,缺点就是太大了...

### 6.2. OpenCV-C++(待完善)
[OpenCV](https://opencv.org/)  
视觉库OpenCV

## 7. Trouble Shooting

### 7.1. pip常见错误
1. http error.这种如果是比较小的包,重试两次,可能可以解决,如果包比较大,复制对应的whl下载下来,然后在对用环境下`pip install xxx.whl`
2. not found,到[pypi](https://pypi.org/)上查找一下这个包是不是存在,是不是你需要的版本,如果没有的话,是不是这个项目有自己封装的包.
3. pip不能安装PyTorch的,requirements.txt里的PyTorch可能会引发异常.PyTorch要用conda安.

### 7.2. conda常见错误
1. http error,同样经常是网络不稳定导致的,建议直接按照命令行自动弹出的whl连接下载后手动安装.
2. 遇事不决换网线,别用wifi.

### 7.3. 依赖/模型下载问题
#### 7.3.1. 判别是否在集群
```
import socket


hostname = socket.gethostname()
at_gpu_cluster = hostname.startswith("terminal") or hostname.startswith("jupyter")
```

上述代码可以用于确定是否在集群环境,如果在集群环境,那么模型的链接可以替换成下属格式(仅作示例):  
```
_url_format_gpu = r"file:///opt/data/public/pretrained_models/resnest/{}-{}.pth"
resnest_model_urls_gpu = {name: _url_format_gpu.format(name, short_hash(name)) for name in _model_sha256.keys()}
```

#### 7.3.2. index server
复杂依赖安装问题其实可以在通过配置脚本进行,上文中设定了可以使用bash脚本后,就可以用wget等从给定链接地址(例如阿里云oss等)获取安装包再安装,python环境设定也可以使用`pip._internal`来单独处理.

setup脚本的工具和样例:
(待更新,预计二月中更新.)

## 8. TBD
+ index server搭建
+ vs c++配置
+ linux常用命令在powershell中的等效
+ 