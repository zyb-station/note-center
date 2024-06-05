# 1 基础配置
## 1.1 用户名及邮箱配置
```
git config --global user.name "username"
git config --global user.email "happy@email.com"
```
## 1.2 仅推动当前分支
```
git config --global push.default simple
```
注：要求 Git 版本 1.9.5 以上
## 1.3 解决 windows 下 git 信息显示乱码的情况
### 1.3.1 让 git 不要管 Winsows/Unix 换行符转换的事
```
git config --global core.autocrlf false
```
### 1.3.2 git 提示信息中文显示正常
```
git config --global core.quotepath false
```
## 1.4 终端 zsh 中的特殊配置
zsh 为 Git 提供了一个 Tab 补全库。 想要使用它，只需在你的 `.zshrc` 中执行 `autoload -Uz compinit && compinit` 即可。
# 2 git 推代码至远端
忽略文件配置一览，可直接用 https://github.com/github/gitignore
## 2.1 生成公钥密钥
```
ssh-keygen -t rsa -C "happy@email.com"		          # 查看pub配置github
```
## 2.2 新仓库将代码推至 GitHub
```
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/zyb-prj/test.git
git push -u origin main
```
## 2.3 已经存在的仓库将代码推至 GitHub
```
git remote add origin https://github.com/zyb-prj/test.git
git branch -M main
git push -u origin main
```
## 2.4 解决推代码时重复输入账号密码的问题
在推代码至远程分支前，运行以下命令配置Git使用钥匙串访问管理器。
```
git config --global credential.helper osxkeychain
```