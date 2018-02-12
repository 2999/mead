#### 关于 CommandLine

为什么能在本地的 terminal 中直接使用 node / npm / git 这些命令（即通过 command line tool 启动这些模块）？甚至配置了本地化命令的 webstorm 也可以直接启动 app？

因为这些模块被放到了 /usr/local/bin 目录下：

![snip20180209_9](https://user-images.githubusercontent.com/1653891/36019732-2a17e1b6-0dbb-11e8-8991-c11c1c6f9f84.png)



注意看上图，甚至有的模块仅是一个软链而已。

/usr/local/bin是环境变量PATH的内容，所以建立软链接后就成为全局命令，就可以被全局使用。

查看环境变量 echo $PATH



#### 如果你使用了某个 bash，比如 zsh，则可以定义 alias

在用户目录下，打开 .zshrc，如下：

![snip20171024_3](https://user-images.githubusercontent.com/1653891/36019788-56911bea-0dbb-11e8-8c1f-ee500bee3479.png)



如上图 ws 这个 alias，其实是指向了全局命令；

比如 subl 则指向了 app 真正的安装目录。