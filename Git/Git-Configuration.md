使用Git的第一件事就是设置你的名字和email,这些就是你在提交commit时的签名，每次提交记录里都会包含这些信息。使用git config命令进行配置：  
```Linux
$ git config --global user.name "Scott Chacon"
$ git config --global user.email "schacon@gmail.com"
```
执行了上面的命令后,会在家目录(/home/shiyanlou)下建立一个叫.gitconfig 的文件（该文件为隐藏文件，需要使用ls -al查看到）. 内容一般像下面这样，可以使用
vim或cat查看文件内容:  
```Linux
$ cat ~/.gitconfig
[user]
        email = schacon@gmail.com
        name = Scott Chacon
```
上面的配置文件就是Git全局配置的文件，一般配置方法是git config --global <配置名称> <配置的值>。  
如果你想使项目里的某个值与前面的全局设置有区别(例如把私人邮箱地址改为工作邮箱)，你可以在项目中使用git config 命令不带 --global 选项来设置. 这会在你当
前的项目目录下创建 .git/config，从而使用针对当前项目的配置。  

既然我们现在把一切都设置好了，那么我们需要一个Git仓库。有两种方法可以得到它：一种是从已有的Git仓库中clone (克隆，复制)；还有一种是新建一个仓库，把未进
行版本控制的文件进行版本控制。  

