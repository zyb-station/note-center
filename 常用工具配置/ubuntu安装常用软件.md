# 1 安装 windterm
## 1.2 详情
- windterm：一款 ubuntu 下的 ssh，debug 等串口工具。
- 官方下载地址：[点击此处跳转至官方下载地址](https://github.com/kingToolbox/WindTerm/releases/tag/2.5.0)
- 解决使用不方便问题
    - 解决问题：使用 WindTerm 打开 tty 设备等串口时，不加 sudo 命令就会碰到权限问题
    - 方便使用：在 Ubuntu 左侧启动栏点击鼠标就启动 WindTerm
## 1.3 安装指南
### 1.3.1 下载并解压软件
1. 下载软件安装包至 ~/Download
2. 解压软件安装包至 ～/software
    ```
    tar -zxvf ~/software WindTerm_2.5.0_Linux_Portable_x86_64.tar.gz
    ```
### 1.3.2 解决权限问题
执行如下命令将用户放入组（diaout、tty 即可），注意用户名 username 根据个人实际情况做改动
```
sudo newgrp dialout tty
```
```
sudo usermod -a -G dialout username
```
```
sudo usermod -a -G tty username
```
### 1.3.3 将软件放入侧边栏
1. 创建 /usr/share/applications/windterm.desktop，文件内容如下: （注意修改配置文件路径，示例中的目录一定要根据个人开发实际情况变更）
    ```
    [Desktop Entry]
    Name=WindTerm
    Comment=A professional cross-platform SSH/Sftp/Shell/Telnet/Serial terminal
    GenericName=Connect Client
    Exec=/home/username/software/WindTerm_2.5.0/WindTerm
    Type=Application
    Icon=/home/zyb/software/WindTerm_2.5.0/windterm.png
    StartupNotify=false
    StartupWMClass=Code
    Categories=Application;Development
    Actions=new-empty-window
    Keywords=windterm
    
    [Desktop Action new-empty-window]
    Name=New Empty Window
    Icon=/home/username/software/WindTerm_2.5.0/windterm.png
    Exec=/home/username/software/WindTerm_2.5.0/WindTerm
    ```
2. 增加文件的可执行权限
    ```
    sudo chmod +x /usr/share/applications/windterm.desktop
    ```
3. 启动软件（没有`./`）
    ```
    /home/username/software/WindTerm_2.5.0/WindTerm
    ```
# 2 安装程序猿计算器
```
sudo snap install uno-calculator
```
# 3 安装常用办公软件
## 3.1 安装搜狗输入法
[点击此处跳转至官方安装指南](https://shurufa.sogou.com/linux/guide)
## 3.2 安装谷歌浏览器
### 3.2.1 下载源
- 官网版本：[chroom浏览器官网版本下载](https://www.google.com/chrome/)
### 3.2.2 下载并安装
1. 下载至指定目录
2. 使用 dpkg 安装
    ```bash
    sudo dpkg -i deb包名
    ```
## 3.3 安装 qq 音乐
### 3.3.1 下载源
- 官网版本：[qq音乐官方版本下载](https://y.qq.com/download/download.html)
### 3.3.2 下载并安装
1. 下载至指定目录
2. 使用 dpkg 安装
    ```
    sudo dpkg -i deb包名
    ```
### 3.3.3 设置启动指令
1. 编辑 ~/.bashrc 文件，添加如下内容
    ```
    ###############################
    ####      qq音乐 启动      ####
    ###############################
    alias qqmusic-start='qqmusic --no-sandbox'
    ```
2. 执行 source 使能
    ```
    source ~/.bashrc
    ```
### 3.3.4 启动 qq 音乐
```
qqmusic-start
```
- 此处执行指令需要根据个人在 ~/.bashrc 中设置的 alias 而定。