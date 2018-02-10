### npm scripts

- 参考：http://www.ruanyifeng.com/blog/2016/10/npm_scripts.html


- 每当执行`npm run`，就会自动新建一个 Shell，在这个 Shell 里面执行指定的脚本命令。因此，只要是 Shell（一般是 Bash）可以运行的命令，就可以写在 npm 脚本里面。

- `npm run`新建的这个 Shell，会将当前目录的`node_modules/.bin`子目录加入`PATH`变量，执行结束后，再将`PATH`变量恢复原样。

  这意味着，当前目录的`node_modules/.bin`子目录里面的所有脚本，都可以直接用脚本名调用，而不必加上路径。比如，当前项目的依赖里面有 Mocha，只要直接写`mocha test`就可以了。

- npm 脚本的唯一要求就是可以在 Shell 执行，因此它不一定是 Node 脚本，任何可执行文件都可以写在里面

- 如果是并行执行（即同时的平行执行），可以使用`&`符号；如果是继发执行（即只有前一个任务成功，才执行下一个任务），可以使用`&&`符号。

### 系统目录

- Linux /usr/bin与/usr/local/bin使用区别：
  - usr 指 `Unix System Resource`，而不是 User
  - /usr/bin下面的都是系统预装的可执行程序，会随着系统升级而改变
  - /usr/local/bin目录是给用户放置自己的可执行程序的地方，推荐放在这里，不会被系统升级而覆盖同名文件
  - 如果两个目录下有相同的可执行程序，谁优先执行受到PATH环境变量的影响，比如我的一台服务器的PATH变量为（echo $PATH）：/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin
  - https://www.jianshu.com/p/ea6c4758dba4
- 当 npm install -g xxx 或 npm link 一个包后，可能会执行两步：1、将包的资源放到 /usr/local/lib/node_modules 下；2、如果在 package.json 中定义了 bin，将 bin 中定义的命令放到 /usr/local/bin 下。如果不同的包定义了相同的命令，则后安装的会覆盖先安装的

### SSH keys

- https://zhidao.baidu.com/question/186653438.html
- ssh keys是远程ssh连接中的一种基于密匙方式安全连接的密匙文件。
- ssh keys是ssh中基于密匙的安全验证，你可以通过创建私人密匙和公用密匙的方式来完成ssh keys方式的ssh登陆验证
  - 首先你必须为自己创建一对密匙，并把公用密匙放在需要访问的服务器上。
  - 如果你要连接到SSH服务器上，客户端软件就会向服务器发出请求，请求用你的密匙进行安全验证。
  - 服务器收到请求之后，先在该服务器上你的主目录下寻找你的公用密匙，然后把它和你发送过来的公用密匙进行比较。
  - 如果两个密匙一致，服务器就用公用密匙加密“质询”（challenge）并把它发送给客户端软件。
  - 客户端软件收到“质询”之后就可以用你的私人密匙解密再把它发送给服务器。
- 基于ssh keys的登陆验证方式可以避免假冒服务器的问题，因为假冒服务器获取不到你的密匙，它比基于用户名密码的口令方式更安全，但是需要的登陆时间也会更长。
- 使用OpenSSH为自己生成一对密钥：`$ ssh-keygen`，完成之后，你应该可以在你的.ssh目录下看到两个文件，id_rsa就是你的私钥，而id_ras.pub则是你的公钥

### 关于证书及密钥：

- 前提：https
- 公钥、私钥、密钥、密钥对、加密密钥、解密密钥、非对称密码、数字签名
- 公钥加密又称为非对称密码，因为加密密钥和解密密钥不一样。慢
- 私钥加密又称为对称加密，因为同一密钥既用于加密又用于解密。快
- 在实际的应用中，人们通常将两者结合在一起使用，例如，对称密钥加密系统用于存储大量数据信息，而公开密钥加密系统则用于加密密钥。
- RSA算法
- 安全传输协议：SSL、TLS
- 证书CA
- 发送https请求前，浏览器先去查找本地对应证书，如果没有，则拒绝请求提示出错
- host优先级是最高的

### 命令行 & 快捷键

- ctrl+A ctrl+E ctrl+w
- man
- cd -
- history 配合 !number
- grep -n 123 *
- Command+Shift+. 可以显示隐藏文件、文件夹，再按一次，恢复隐藏；
- finder下使用Command+Shift+G 可以前往任何文件夹，包括隐藏文件夹
- sudo su admin ：转换成admin身份
- sudo su root：转换成超级管理员身份
- sudo […] : 临时获取admin权限(在某个账号下使用时)
- ln -s [sourse] [target] ：符号链接
- man ln 或 ln —help ：查文档
- pwd ：查看当前路径
- touch [fileName]: 新建一个文件
- exit : 退出admin身份
- vim：查看或编辑某个文件
- ls -alh：查看用户对文件的操作权限
- chmod：修改某用户或组对文件的操作权限（http://www.[cnblogs.com/avril/archive/2010/03/23/1692809.html）](http://cnblogs.com/avril/archive/2010/03/23/1692809.html%EF%BC%89)
- sudo chmod 777 file ： 置为可读
- cat package.json | grep version，即可看到模块的版本号。解释：cat package.json 会把 package.的所有内容打印到标准输出，后面跟上|，是一个管道操作，表示把上一条命令的标准输出作为下一条命令的标准输入。即：使用 grep 去查找 cat pacjson 输出的内容里的 version 关键字。也可以用 grep version package.json ，更简单，性能也更好一些。
- npm list -g --depth=0：查看本地安装的所有的nam模块及版本号，--depth=1可以看1级依赖，依次类推。同理，也可以用tnpm list -g --depth=0
- [[：移动到文件头
- ]]：移动到文件尾
- ctrl+f：向下翻一屏
- ctrl+b：向上翻一屏
- ctrl+u：向上滚动半屏
- ctrl+d：向下滚动半屏
- $：移动到行尾
- ^：移动到行首
- :set nu：设置行号
- /xxx：查找xxx，按n健查找下一个，按N健查找前一个
- 复制一行：把光标移动到要复制的行上按yy，把光标移动到要复制的位置按p
- sudo echo limit maxfiles 100000 100000|sudo tee -a /etc/launchd.conf
  - restart computer
- tnpm root -g
- cd `npm root -g`
- /Users/与/usr/；/usr/local/bin、/usr/local/lib；/usr/lib
- shell中command + k
- 查看某类本地进程：ps -ef | grep node
- 杀死某个进程：sudo kill -9 11808
- command + shift + v：mac去格式粘贴；
- Command + L：mac如何使用快捷键将 Chrome 浏览器光标定位到地址栏；