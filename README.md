# GZY_ChatRoom GZY聊天室
 这是一个用python编写的多人聊天室+文件服务器。
 
 This is an ultra-small multiplayer chat room + file server written in Python.

 本项目包含以下内容：
 
1. 一个超小型的python聊天服务器，部署方便，使用简单。
2. 一个UI界面设计得十分简陋但是能用的客户端，用于对接python服务器。
3. 一个迷你的python文件服务器（类似网盘），可以实现查看、上传和下载文件功能，自带哈希校验保证文件完整性。

## 项目目录
- [项目介绍](#项目介绍)
- [安装](#安装)
 - [源码安装](#源码安装)
 - [可执行文件安装](#可执行文件安装)
- [使用说明](#使用说明)
 - [聊天功能](#聊天功能)
 - [文件传输功能](#文件传输功能)
 - [其他注意事项](#其他注意事项)
- [示例](#示例)
- [维护者](#维护者)
- [如何贡献](#如何贡献)
- [使用许可](#使用许可)

## 项目介绍
 本项目是使用python编写的聊天室，集成了文件服务器的功能，能够实现文件的上传和下载。
 
 项目优点：
 - 体积较小，占用资源少，非常适合轻量级Arm设备部署。
 - 源码简单易懂，适合网络编程的学习。
 - 虽然UI界面简陋，但可以实现关键的功能，足够使用。
 - 源码依赖的东西较少，大部分网络操作使用python原生的socket库实现，部署时出现不兼容的情况几乎没有。
 
 项目缺点：
 - 功能太少，而且有些功能不完善，有些代码没有经过优化，存在隐藏的bug，请谨慎使用。（作者水平不足，但已经尽力增加完整的异常处理机制，按手册正常使用不会出现问题。）
 - 界面简陋，操作较为复杂。（需要记忆简单的中文指令）
 - 不支持内网穿透，推荐在拥有公网IP的服务器上部署，或采用[coplar](https://www.cpolar.com/)进行内网穿透。（也可采用其他方法进行内网穿透）
 
## 安装
 可以采用如下两种方案部署服务器：源码安装和可执行文件安装。
### 源码安装
1. 克隆项目到本地：

```sh
$ git clone https://github.com/JiaXinSugar-114514/GZY_ChatRoom.git
```

2. 进入项目目录：

```sh
$ cd GZY_ChatRoom
```

3. 配置Python环境：

  请首先安装Anaconda，如果没有安装Anaconda可以跳过创建虚拟环境这一步。

- 创建并激活虚拟环境：

```sh
$ conda create -n gzy python=3.10
$ conda activate gzy
```

- 安装依赖
    - 如果您在国外，可以直接运行如下指令安装：
    ```sh
    $ pip install -r requirements.txt
    ```
    - 如果您在国内，可以考虑通过镜像源安装：
    ```sh
    $ pip install -r requirements.txt -i https://pypi.mirrors.ustc.edu.cn/simple/
    ```
     
4. 运行：

- 如果你想运行服务器，请输入如下命令：

```sh
$ python ./Server/Server.py
```

- 如果你想运行客户端，请输入如下命令：

```sh
$ python ./Client/Client.py
```

### 可执行文件安装
 如果您对如何配置Python环境不了解，可以考虑直接运行可执行文件进行部署，以下是部署方法：
- Windows平台：

  如果您的服务器平台是Windows系统，且CPU指令集是X86，可以直接运行项目目录下的Server&Client_Windows_amd64文件夹内的后缀为exe的可执行文件来部署。
  
  ```sh
  D:\>Server&Client_Windows_amd64/Server.exe
  #部署服务器
  D:\>Server&Client_Windows_amd64/Client.exe
  #部署客户端
  ```
  
  其他指令集架构的CPU请使用源码安装。
  
- Linux平台：
  如果您的服务器平台是Linux系统，且CPU架构是arrch64(Arm64)，可以考虑运行项目目录下的Server_Linux_Debain_arrch64文件夹内的Server文件来部署服务器。
  
  ```sh
  $ cd Server_Linux_Debain_arrch64
  #进入可执行文件目录
  $ chmod +x Server
  #赋予可执行权限
  $ ./Server
  #运行服务器
  ```
  
  暂时没有对x86及其他平台进行适配，请使用源码安装方式部署。
  对于轻量级Arm设备，没必要运行带有图形界面的客户端，如需运行请使用源码进行安装。

## 使用说明

  以下是聊天室的使用说明书
  
### 聊天功能

- 启动服务器后，服务器会自动选取服务器自身的IP地址进行监听，端口号默认为510，可以自行在源码设置。
- 打开客户端后，在上方的IP和Port文本框内输入服务器的IP地址和端口，按下Connect即可连接成功，如果连接失败会报告错误。
  __注意请不要关闭客户端附带的黑色命令行窗口！ 该窗口也可以用于监视客户端实时状态。__
- 刚连接服务器后请先在下方文本框内输入您的上网昵称，接着按下右下角的Send按钮进行发送，或勾选右上角的回车发送，按下回车即可设置昵称，接着会接收聊天记录，请耐心等待接收完毕。
- 完成以上步骤后即可在下方文本框内输入文本聊天了，支持简单的emoji表情，关闭回车发送后可以进行多行输入。
- 如果想发送图片，可以按下右下角的File按钮，选择图片后即可将图片发送至服务器，接着会自动将图片显示在聊天框内。
- __请注意！在聊天结束后，请先按下右上角的Disconnect按钮，再关闭客户端的命令行窗口，即可正常退出聊天室。__

### 文件传输功能

- 上传文件的方法和发送图片一致，唯一不同的是发送文件不会显示在聊天框内，只会有提示。
  文件会保存在服务器目录下的Cloud文件夹中。
- 如果想查看目前服务器端保存的文件，请在文本框内输入以下指令发送即可：
  ```sh
  ！查看文件
  ```
  __请注意，指令中的感叹号是中文感叹号！__
  
- 如果想对某个文件进行下载，请输入以下指令：
  ```sh
  ！下载文件*文件名
  ```
  __请注意！指令中的感叹号是中文感叹号，文件名和指令间要用*符号隔开，文件名必须带后缀。__
  
  例如：
  ```sh
  ！下载文件*gzy.jpg
  ```
  这样就可以将服务器上的gzy.jpg文件下载下来，文件会保存在客户端目录下的Recv文件夹内。
  
  __上传和下载文件的过程都是自带哈希校验的，确保文件的完整性，如果因为网络原因文件不完整，会提示上传或下载失败，此时请更换网络重新尝试。__
  
### 其他注意事项
  还有几点其他服务器的特性需要阐述清楚。
- 服务器会将日志文件存放在服务器目录下面的log.txt 文件中，没有自动删除日志文件的功能，请定期清理日志。
- 客户端如果长时间未收到服务器发来消息，会自动断开连接，这个时间默认为10分钟。
- 服务器会保存最新的10条聊天记录，超出10条的记录自动删除，这10条记录会自动发送给刚刚建立连接的客户端。但可以在服务器日志中查看完整的聊天记录。

## 示例
以下是聊天室的客户端界面示例：

![image](https://github.com/JiaXinSugar-114514/GZY_ChatRoom/blob/main/Example.png)

## 维护者
  该项目目前由我（小阳）独自维护，如果您有任何问题希望和我联系，可以通过以下途径：
  - 通过邮件：
    我的邮箱：jiaxinsugar@gmail.com
  - 通过QQ群：
    我的QQ群：903448967
  
## 如何贡献
  欢迎大佬Pull requests，也可以联系我进行贡献。
  
## 使用许可
  本项目采用MIT license，遵循该许可即可。（基本无任何限制了这个协议...）
  
  
  











 
 
