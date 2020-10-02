<!-- ## environment variable and java system variable and command line argument  区别 -->
- [概述](#%E6%A6%82%E8%BF%B0)
- [os 变量](#os-%E5%8F%98%E9%87%8F)
- [java system variable](#java-system-variable)
- [命令行参数](#%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%8F%82%E6%95%B0)
- [总结](#%E6%80%BB%E7%BB%93)

### 概述
java中可从 os environment 和 java system variable 和 命令行参数 读取 属性值,
 * os envionment 是系统层面(可以同一机器上进程中共享)
 * java system variable 是 jvm 提供的系统变量 
 * 命令行参数 命令行的参数 如(./test.shell  parameter1 parameter2)

### os 变量
os environment 是系统环境,在linux shell 中输入env.
```shell
➜  ~ env
LC_ADDRESS=zh_CN.UTF-8
XDG_CONFIG_DIRS=/etc/xdg/xdg-ubuntu:/etc/xdg
LC_TELEPHONE=zh_CN.UTF-8
LANG=en_US.UTF-8
DISPLAY=:1
SHLVL=1
LOGNAME=lh
XDG_VTNR=2
```
java 可得到相同的结果通过 
```java
public static void main(String[] args) {
	System.getenv();
}
```
linux 中可以在
/etc/profile
/etc/environment
～/.bashrc
三个文件中配置 os environment.

>配置语法如下:
```shell
export JAVA_HOME=/usr/local/jdk1.8.0_91
export CLASSPATH=..:$JAVA_HOME/lib:$JAVA_HOME/jre/lib
``` 

### java system variable
java system variable  是 java 运行时可读取的属性值.
一些重要的属性:

| key  |  value |
|---|---|
|"file.separator"|	Character that separates components of a file path. This is "/" on UNIX and "\" on Windows.|
|"java.class.path"|	Path used to find directories and JAR archives containing class files. Elements of the class path are separated by a platform-specific character specified in the path.separator property.|
|"java.home"|	Installation directory for Java Runtime Environment (JRE)|
|"java.vendor"|	JRE vendor name|
|"java.vendor.url"|	JRE vendor URL|
|"java.version"|	JRE version number|
|"line.separator"|	Sequence used by operating system to separate lines in text files|
|"os.arch"|	Operating system architecture|
|"os.name"|	Operating system name|
|"os.version"|	Operating system version|
|"path.separator"|	Path separator character used in java.class.path|
|"user.dir"|	User working directory|
|"user.home"|	User home directory|
|"user.name"|	User account name|

可以通过命令行参数来添加属性:

```shell
 java -jar -Denv=DEV  user-web-1.0.jar
```

也可以通过java 来添加:
```java
public static void main(String[] args) {
	System.getProperties().setProperty("testKey","testValue");
}
```

### 命令行参数
在shell 脚本的概念中有命令行参数的概念
```shell
./test.shell  parameter1 parameter2
```
在上述执行脚本中 test.shell 里可以通过 $1和$2 获取参数  parameter1和parameter2.
在 java中也有相同的概念,在获取参数的方式上有所区别
```java
class CommandLineExample {
    public static void main(String args[]) {
		System.out.println("Your first argument is: " + Arrays.toString(args));
    }
}
```
通过 args[] 数组结合来获取参数.

### 总结
一般java  属性配置 优先级 command-line argument > system properties > os environment.

命令行参数 在脱离java 的认知层面中是最自由的所有和别的系统交互等场景 最好使用 command-line argument.
system properties 也可以通过 java -D 来添加,不过面对层面 就只有java 命令 里参数的层面了.
