# Deepin

安装jdk8, 使用:

`update-alternatives --config java`

来切换多版本jdk

或

` apt install openjdk-8-jdk`







更改root密码：

在系统文件中的cmdline文件后添加

`init=/bin/bash`

再在pi的开机界面输入：

mount -o remount , rw / passwd pi

sudo passwd root





` 使用命令行：java （class）`

无法加载类：

解决办法：在外层使用 package.classname 的形式访问
