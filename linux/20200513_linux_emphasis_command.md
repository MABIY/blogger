<!-- ## linux  牢记命令 -->
- [find command](#find-command)
- [rm command](#rm-command)
- [lsof command](#lsof-command)
### find command
> 样例命令:

搜索当前运行脚本目录下 以jar 结尾的 文件并解压到对应的 名字命名的文件夹中.

查询待执行的命令:
```shell
➜  ~ find *.jar -exec sh -c 'exec unzip -o -d "${0%.*}" "$0"'  {} \;
result:
unzip -o -d ./user-resource-tools-1.0.29-20200506.085300-4 ./user-resource-tools-1.0.29-20200506.085300-4.jar
unzip -o -d ./user-resource-web-1.0-SNAPSHOT ./user-resource-web-1.0-SNAPSHOT.jar

```
执行命令:
```shell
➜  ~  find -name '*.jar' -exec sh -c 'unzip -o -d "${0%.*}" "$0"'  {} \;
result:
user-passport-web-1.0-SNAPSHOT.jar
user-resource-web-1.0-SNAPSHOT
user-resource-tools-1.0.29-20200506.085300-4.jar
user-resource-tools-1.0.29-20200506.085300-4
```
> 命令解释:

分两部分理解:
* 第一部分:
```shell
   find -name '*.jar'; 
```
查询当前执行该shell执行目录里名字匹配 *.jar 的文件.

* 第二部分:

```shell
    -exec sh -c 'unzip -o -d "${0%.*}" "$0"'  {} \;
```
在 find -exec 中 通过 {} 来获取 find -name '*.jar' 命令的结果 -> files;
在 sh-c 中 通过 `${0%.*}` `$0` 来取得 files 集合中的每个一个文件值来执行解压;
`\;` 的作用是转义不让shell解析,以此传给 -exec 识别来结束-exec执行;


### rm command
> 样例命令:

删除执行这个命令目录里所有的目录文件夹.

```shell
rm -R `ls -1d */`
```

### lsof command
> 样例命令:

查询pid 监听的 端口
```shell
➜  ~ lsof -i|grep 1963
java       1963   lh   45u  IPv6 865015      0t0  TCP *:8037 (LISTEN)
java       1963   lh   46u  IPv6 865016      0t0  TCP *:8009 (LISTEN)
java       1963   lh   48u  IPv6 865019      0t0  TCP localhost:8005 (LISTEN)
```
查询端口对应的pid
```shell
➜  ~ lsof -i:8009
COMMAND  PID USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
java    1963   lh   46u  IPv6 865016      0t0  TCP *:8009 (LISTEN)
➜  ~ lsof -i:8037
COMMAND  PID USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
java    1963   lh   45u  IPv6 865015      0t0  TCP *:8037 (LISTEN)
```