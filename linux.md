# linux 常用命令

## 目录结构

* `/bin` ：`bin`是`Binary`的缩写, 这个目录存放着最经常使用的命令。
* `/boot` : 这里存放的是启动`Linux`时使用的一些核心文件，包括一些连接文件以及镜像文件。
* `/dev` : dev是`Device(设备)`的缩写, 该目录下存放的是`Linux`的外部设备，在`Linux`中访问设备的方式和访问文件的方式是相同的。
* `/etc` : 这个目录用来存放所有的系统管理所需要的配置文件和子目录。
* `/home` : 用户的主目录，在`Linux`中，每个用户都有一个自己的目录，一般该目录名是以用户的账号命名的。
* `/lib` : 这个目录里存放着系统最基本的动态连接共享库，其作用类似于`Windows`里的`DLL`文件。几乎所有的应用程序都需要用到这些共享库。
* `/lost+found` : 这个目录一般情况下是空的，当系统非法关机后，这里就存放了一些文件。
* `/media` : `linux`系统会自动识别一些设备，例如U盘、光驱等等，当识别后，`linux`会把识别的设备挂载到这个目录下。
* `/mnt` : 系统提供该目录是为了让用户临时挂载别的文件系统的，我们可以将光驱挂载在`/mnt/`上，然后进入该目录就可以查看光驱里的内容了。
* `/opt` : 这是给主机额外安装软件所摆放的目录。比如你安装一个`ORACLE`数据库则就可以放到这个目录下。默认是空的。
* `/proc` : 这个目录是一个虚拟的目录，它是系统内存的映射，我们可以通过直接访问这个目录来获取系统信息。
这个目录的内容不在硬盘上而是在内存里，我们也可以直接修改里面的某些文件，比如可以通过下面的命令来屏蔽主机的`ping`命令，使别人无法`ping`你的机器: `echo 1 > /proc/sys/net/ipv4/icmp_echo_ignore_all`
* `/root` : 该目录为系统管理员，也称作超级权限者的用户主目录。
* `/sbin` : `s`就是`Super User`的意思，这里存放的是系统管理员使用的系统管理程序。
* `/selinux` : 这个目录是`Redhat/CentOS`所特有的目录，`Selinux`是一个安全机制，类似于`windows`的防火墙，但是这套机制比较复杂，这个目录就是存放`selinux`相关的文件的。
* `/srv` : 该目录存放一些服务启动之后需要提取的数据。
* `/sys` : 这是`linux2.6`内核的一个很大的变化。该目录下安装了`2.6`内核中新出现的一个文件系统 `sysfs` 。
`sysfs`文件系统集成了下面3种文件系统的信息：针对进程信息的`proc`文件系统、针对设备的`devfs`文件系统以及针对伪终端的`devpts`文件系统。
该文件系统是内核设备树的一个直观反映。
当一个内核对象被创建的时候，对应的文件和目录也在内核对象子系统中被创建。
* `/tmp` : 这个目录是用来存放一些临时文件的。
* `/usr` : 这是一个非常重要的目录，用户的很多应用程序和文件都放在这个目录下，类似于`windows`下的`program files`目录。
* `/usr/bin` : 系统用户使用的应用程序。
* `/usr/sbin` : 超级用户使用的比较高级的管理程序和系统守护程序。
* `/usr/src` : 内核源代码默认的放置目录。
* `/var` : 这个目录中存放着在不断扩充着的东西，我们习惯将那些经常被修改的目录放在这个目录下。包括各种日志文件。
* `/run` : 是一个临时文件系统，存储系统启动以来的信息。当系统重启时，这个目录下的文件应该被删掉或清除。如果你的系统上有 `/var/run` 目录，应该让它指向 `run`。

## 常用命令

### scp
> 进行文件安全复制
```shell
  scp [可选参数] file_source file_target 

  -1： 强制scp命令使用协议ssh1
  -2： 强制scp命令使用协议ssh2
  -4： 强制scp命令只使用IPv4寻址
  -6： 强制scp命令只使用IPv6寻址
  -B： 使用批处理模式（传输过程中不询问传输口令或短语）
  -C： 允许压缩。（将-C标志传递给ssh，从而打开压缩功能）
  -p：保留原文件的修改时间，访问时间和访问权限。
  -q： 不显示传输进度条。
  -r： 递归复制整个目录。
  -v：详细方式显示输出。scp和ssh(1)会显示出整个过程的调试信息。这些信息用于调试连接，验证和配置问题。
  -c cipher： 以cipher将数据传输进行加密，这个选项将直接传递给ssh。
  -F ssh_config： 指定一个替代的ssh配置文件，此参数直接传递给ssh。
  -i identity_file： 从指定文件中读取传输时使用的密钥文件，此参数直接传递给ssh。
  -l limit： 限定用户所能使用的带宽，以Kbit/s为单位。
  -o ssh_option： 如果习惯于使用ssh_config(5)中的参数传递方式，
  -P port：注意是大写的P, port是指定数据传输用到的端口号
  -S program： 指定加密传输时所使用的程序。此程序必须能够理解ssh(1)的选项。
```

例:
* 本地到远程
  `scp local_file remote_username@remote_ip:remote_folder `
* 远程到本地
  `scp remote_username@remote_ip:remote_folder local_file `