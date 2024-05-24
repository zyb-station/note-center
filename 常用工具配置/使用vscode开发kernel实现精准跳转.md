**目标：实现内核代码精准跳转**
# 1 软件安装
## 1.1 基础软件安装
- 安装并配置 git：参考 [[git快捷配置]]
- 安装 bear 工具（用于生成钩子）：`sudo apt install bear`
- 安装 vscode 及其插件，详情参考[[#1.2 安装 vscode 及其插件]]。
## 1.2 安装 vscode 及其插件
### 1.2.1 安装 vscode
- 官网下载：[点击此处跳转至下载位置](https://code.visualstudio.com/)
### 1.2.2 vscode 插件安装
- c 技术栈类：`C/C++`    `C/C++ Extension Pack`    `C/C++ Snippets`    `Clangd` `Code Runner`  
- linux 开发工具类：`Remote SSH`    `DeviceTree`    `Arm Assembly`    `Hex Editor`
- 软件开发工具类：`Code Spell Checker`     `compareit`    `Tabnine AI Autocomplete`    `Bracket Pair Colorization Toggler` 
- 辅助开发工具类：`Chinese`     `vscode-icons`    `One Dark Pro`    `Rainbow Highlighter` ： 高亮文字：shift + alt + z     取消高亮：shift + alt + a            
- markdown类：`Markdown All in One`    `Markdown Preview Enhanced`
## 1.3 安装 clangd
vscode 安装 clang 插件后，还需要一个运行在 Linux 服务器上的 clangd 程序。原因是我们使用 vscode 打开 c 文件时，vscode 会提示你安装 clangd 程序，它会安装最新版本(版本15)，但是这个版本有 Bug，所以需要手工安装版本 13。
### 1.3.1 下载源
- 官方下载地址：[Clang13.0官方版本下载](https://github.com/clangd/clangd/releases/tag/13.0.0)
- 个人维护版本：[Clang13.0个人维护版本下载](https://zyb-software-center.oss-cn-chengdu.aliyuncs.com/linux/ubuntu/clangd-linux-13.0.0.zip?OSSAccessKeyId=LTAI5tREkNKGRcMiPdgNQUye&Expires=10000000001701340000&Signature=OXsecHyMZlRu2VKVjLg%2Fi3E6Dvs%3D)
### 1.3.2 下载并安装（一定要在服务端安装）
1. 需要安装 clang 插件
2. 下载 clang13.0 版本至指定目录
3. 把下载到的 clangd-linux-13.0.0.zip 放到指定目录下，此处为 ~/software
    ```bash
    unzip -d ~/software clangd-linux-13.0.0.zip
    ```
# 2 使用 vscode 远程连接
## 2.1 基本要求
- 确保 ubuntu 服务端安装了 ssh 以及 net-tools
    ```bash
    sudo apt-get install ssh net-tools
    ```
- 确保 ubuntu 服务端 ubuntu 下的 vscode 安装了 Remote SSH 插件，同时客户端的 vscode 也安装了 Remote SSH 插件。
- linux 内核开发建议使用 ubuntu 操作系统来做开发，下面我们称其为服务端。同时 windows 或 mac 操作系统更具有可操作性，下面称其为客户端，因此我们可以在 win 或 mac 下使用 vscode 远程连接服务器来做开发。
## 2.2 vscode 使用 ssh 连接
1. 获取服务端 IP，假设为 xx.xx.xx.x。
2. 打开服务端 vscode，点击左下角的远程连接按钮。
3. 首次需要点击新增连接，后续直接点击添加好的服务器 ip 即可。
4. 按要求配置远程连接指令：`ssh username@xx.xxx.xxx.x -A`，输入完成后按回车确定。
5. 重新按照 1st & 2nd & 3rd 的方式走到 3rd 所示途中的位置会出现添加的配置，点击即可连接。
6. 客户端登录免密登陆。
- 生成客户端密钥，参考[[git快捷配置#2.1 生成公钥密钥]]。
- 使用`ssh-copy-id -p 端口号 username@ip`指令（端口号默认22可以不用写）将本地客户端公钥复制到服务端的`~/.ssh/authorized_keys` 文件中。
7. 回到 4th 步，打开 vscode 在 4th 中设置的 config 文件，对应配置方式如下，配置完成之后保存即可。
	```shell
        Host xx.xxx.xx.xx
          HostName xx.xxx.xx.xx
          User 主机名
          Port 端口号
          IdentityFile ~/.ssh/id_rsa
    ```
8. 远程连接成功之后一定将插件在远程也安装一份，直接打开插件然后在本地模块往下拉到插件 ssh 区域，看到黄色感叹号点击即可安装在远端。
# 3 服务端配置
1. 确保 clang13.0 插件完成安装，详情参考[[#1.3 安装 clangd]]，并获取其安装路径（此处为 ～/software/clangd_13.0.0/bin）。
2. 修改服务端设置文件，客户端 vscode 连接到服务端之后打开 vscode 服务器配置文件 settings.json 做适当调整。settings.json 基本设置内容如下：
    ```json
    {
    	"C_Cpp.default.intelliSenseMode": "linux-gcc-arm",
    	"C_Cpp.intelliSenseEngine": "Disabled",
    	"clangd.path": " /.../clangd_13.0.0/bin/clangd",
    	"clangd.arguments": [
    		"--log=verbose",
    	],
    }
    ```

