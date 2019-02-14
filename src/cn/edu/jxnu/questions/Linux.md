### Linux基础

#### 工作环境设置文件与环境变量

环境设置文件有两种：系统环境设置文件和个人环境设置文件

1. 系统中的用户工作环境设置文件：

* 登录环境设置文件：```/etc/profile ```   
* 非登录环境设置文件：```/etc/bashrc```

2. 用户个人设置的环境设置文件：
 
* 登录环境设置文件: ```$HOME/.bash_profile```   指用户登录系统后的工作环境  //这个是环境变量设置的地方
* 非登录环境设置文件：```$HOME/.bashrc```       指用户再调用子shell时所使用的用户环境  //这个是定义别名的地方

```vi ~/.bash_profile``` 修改PATH行,把环境变量添加进去，这种方法是针对用户起作用的

我的电脑的环境变量：

打开 vi ~/.bash_profile 

    export M2_HOME=/Users/liguobin/soft/maven
    export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_191.jdk/Contents/Home
    export GRADLE_HOME=/Users/liguobin/soft/gradle
    export TOMCAT_HOME=/Users/liguobin/soft/tomcat
    export ANDROID_HOME=/Users/liguobin/soft/android-sdk-macosx
    export PATH=$PATH:$GRADLE_HOME/bin:$JAVA_HOME/bin:$M2_HOME/bin:$TOMCAT_HOME/bin:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools

冒号隔开；```$M2_HOME```表示引用变量；
查看环境变量：```echo $PATH```；
修改完刷新：```source ~/.bash_profile```，不报错则成功。

#### Linux常用命令

```//后面是追加注释```

* 查找文件

```find / -name filename.txt``` //根据名称查找/目录下的filename.txt文件<br>
```find . -name "*.xml"``` //递归查找所有的xml文件<br>
```find . -name "*.xml" |xargs grep "hello world"``` //递归查找所有文件内容中包含hello world的xml文件<br>
```grep -H 'spring' *.xml``` //查找所以有的包含spring的xml文件<br>
```find ./ -size 0 | xargs rm -f & ``` //删除文件大小为零的文件<br>
```ls -l | grep '.jar'``` //查找当前目录中的所有jar文件<br>
```grep 'test' d*``` //显示所有以d开头的文件中包含test的行<br>
```grep 'test' aa bb cc``` //显示在aa，bb，cc文件中匹配test的行<br>
```grep '[a-z]\{5\}' aa``` //显示所有包含每个字符串至少有5个连续小写字符的字符串的行<br>
```lesss fileName``` //  / 向下搜索 ？向上搜索 &/ 只显示匹配模式的行<br>

* 查看一个程序是否运行

```ps –ef|grep tomcat``` //查看所有有关tomcat的进程<br>
```ps -ef|grep --color java``` //高亮要查询的关键字<br>

* 终止线程

```kill -9 19979``` //终止线程号位19979的进程

* 查看文件，包含隐藏文件

```ls -al```

* 当前工作目录

```pwd```

* 复制文件

```cp source dest``` //复制文件<br>
```cp -r sourceFolder targetFolder``` //递归复制整个文件夹<br>
```scp sourecFile romoteUserName@remoteIp:remoteAddr``` //从本地拷贝到远程<br>
```scp remote_username@remote_ip:remote_folder  local_folder``` //从远处复制到本地<br>

* 创建目录

```mkdir newfolder```

* 删除目录

```rmdir deleteEmptyFolder``` //删除空目录<br>
```rm -rf deleteFile``` //递归删除目录中所有内容<br>

* 移动文件

```mv /temp/movefile /targetFolder```

* 重命名命令

```mv oldNameFile newNameFile```

* 切换用户

```su -username```

* 修改文件权限

```chmod 777 file.java``` //file.java的权限-rwxrwxrwx，r表示读、w表示写、x表示可执行

* 压缩文件

```tar -czf test.tar.gz /test1 /test2```

* 列出压缩文件列表

```tar -tzf test.tar.gz```

* tar解压文件

```tar -xvzf test.tar.gz```

* zip命令压缩并排除某一目录

```zip -r 2019-02-12-19-30-00.zip ./ -x "./log/*"``` //使用zip压缩文件，将当前目录的所有文件/文件夹压缩成为2019-02-12-19-30-00.zip，并且排除掉当前文件夹中的log文件夹。

* 查看文件头10行

```head -n 10 example.txt```

* 查看文件尾10行

```tail -n 10 example.txt```

* 查看日志类型文件

```tail -f exmaple.log``` //这个命令会自动显示新增内容，屏幕只显示10行内容的（可设置）。

* 使用超级管理员身份执行命令

```sudo rm a.txt``` //使用管理员身份删除文件

* 查看端口占用情况

```netstat -tln | grep 8080``` //查看端口8080的使用情况

* 查看端口属于哪个程序

```lsof -i :8080```

* 查看进程

```ps aux|grep java``` //查看java进程<br>
```ps aux``` //查看所有进程<br>

* 以树状图列出目录的内容

```tree a```

在Mac OSX 系统默认是没有类似windows中的 tree命令，找到一条比较有意思的命令可以实现：<br>
```find . -print | sed -e 's;[^/]*/;|____;g;s;____|; |;g'```<br>
为了方便使用，写一个alias 到~/.profile里:<br>
```alias tree="find . -print | sed -e 's;[^/]*/;|____;g;s;____|; |;g'"```写完记得```source ~/.profile```

* 文件下载

```wget http://file.tgz```  //mac下安装wget命令<br>
```curl http://file.tgz```<br>

* 网络检测

```ping www.just-ping.com``` //加参数-t表示持续进行

* 远程登录

```ssh userName@ip```

* ```>>```和```>```重定向命令

```>``` 是定向输出到文件，如果文件不存在，就创建文件；如果文件存在，就将其清空；一般我们备份清理日志文件的时候，就是这种方法：先备份日志，
再用 ```>```，将日志文件清空（文件大小变成0字节）。

```>>``` 这个是将输出内容追加到目标文件中。如果文件不存在，就创建文件；如果文件存在，则将新的内容追加到那个文件的末尾，该文件中的原有内容不受影响

* java 常用命令

java, javac, [jps](http://www.hollischuang.com/archives/105), [jstat](http://www.hollischuang.com/archives/481), 
[jmap](http://www.hollischuang.com/archives/303), [jstack](http://www.hollischuang.com/archives/110)

* 输出

```var=$(echo 1)``` //获取echo输出的值，并赋值给变量；或使用``` `` ```<br>
```awk '{print $2}' $fileName ``` //一行一行的读取指定的文件， 以空格作为分隔符，打印第二个（列）字段<br>

* 发送curl，并判断返回值是否为空

```
#返回类型：application/json get
result=$(curl-G http://www.ss.com)
if [! -n "$result" ];then
	echo"成功！"
else
	echo $result
fi 
```

* Mac获取当前时间戳

```date +%s``` 赋值```CURRENT_TIME=$(date+%s)```

* 后台进程

在后台启动 ```sh runMaxim.sh &```

进程切换到后台的时候，我们把它称为job。切换到后台时会输出相关job信息，<br>
以前面的输出为```[1] 11319 [1]表示job ID是1，11319表示进程ID是11319。切换到后台的进程，仍然可以用ps命令查看。```<br>
 
前后台间切换可以通过```bg <jobid> (background)```和```fg<jobid>()foreground)```命令将其在前后台间状态切换。

* 其他命令

        which：which 可执行文件名称（which是通过 PATH环境变量到该路径内查找可执行文件，所以基本的功能是寻找可执行文件 ）
        whereis：whereis 文件或者目录名称（从数据库文件中查找，不是实时更新）

* linux命令学习网站:

[linux命令](http://explainshell.com/)

参考资料：

[Linux端口被占用的解决(Error: JBoss port is in use. Please check](http://www.hollischuang.com/archives/239)|
[linux 中强大且常用命令：find、grep](https://linux.cn/article-1672-1.html)|
[mac下安装wget命令](http://www.hollischuang.com/archives/548)

主要是工作中收集的，以及www.hollischuang.com中收录的。