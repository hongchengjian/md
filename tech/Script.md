# Kettle ETL

# Python Flask、Django



# Go

```shell
 /******************************************************************************
  * Go 编译器命令
  *****************************************************************************/
go command [arguments]                              // go 命令 [参数]
go build                                            // 编译包和依赖包
go clean                                            // 移除对象和缓存文件
go doc                                              // 显示包的文档
go env                                              // 打印go的环境变量信息
go bug                                              // 报告bug
go fix                                              // 更新包使用新的api
go fmt                                              // 格式规范化代码
go generate                                         // 通过处理资源生成go文件
go get                                              // 下载并安装包及其依赖
go install                                          // 编译和安装包及其依赖
go list                                             // 列出所有包
go run                                              // 编译和运行go程序
go test                                             // 测试
go tool                                             // 运行给定的go工具
go version                                          // 显示go当前版本
go vet                                              // 发现代码中可能的错误

/*******************************************************************************
* ENV
*******************************************************************************/
GOOS                                                  // 编译系统
GOARCH                                                // 编译arch
GO111MODULE                                           // gomod开关
GOPROXY                                               // go代理 https://goproxy.io  https://goproxy.cn
GOSSAFUNC                                             // 生成SSA.html文件，展示代码优化的每一步 GOSSAFUNC=func_name go build

/*******************************************************************************
 * Hello World
 ******************************************************************************/
// main.go
package main                                        // 包名

import "fmt"                                        // 导入fmt包

func main() {                                       // 主函数
    fmt.Println("Hello World")                      // 打印输出
}
// go run main.go                                   // 直接运行
// go build && ./main                               // 先编译成二进制文件再运行



/*******************************************************************************
 * 操作符
 ******************************************************************************/
// 算数操作符
+ - * / %                                           // 加 减 乘 除 取余
& | ^ &^                                            // 位与 位或 位异或 位与非
<< >>                                               // 左移 右移
// 比较操作
== !=                                               // 等于 不等于
< <=                                                // 小于 小于等于
> >=                                                // 大于 大于等于
// 逻辑操作
&& || !                                             // 逻辑与 逻辑或 逻辑非
// 其他
& * <-                                              // 地址 指针引用 通道操作



/*******************************************************************************
 * 声明
 ******************************************************************************/
a := 1                                              // 直接给一个未声明的变量赋值
var b int                                           // var 变量名 数据类型 来声明
var c float64
// 注意：使用var声明过的变量不可再使用 := 赋值
a = 2
const d = 1                                         // 常量




/*******************************************************************************
 * 数据类型
 ******************************************************************************/
s := "hello"                                       // 字符
a := 1                                             // int
b := 1.2                                           // float64
c := 1 + 5i                                        // complex128
// 数组
arr1 := [3]int{4, 5, 6}                           // 手动指定长度
arr2 := [...]int{1, 2, 3}                         // 由golang自动计算长度
// 切片
sliceInt := []int{1, 2}                           // 不指定长度
sliceByte := []byte("hello")
// 指针
a := 1
point := &a                                      // 将a的地址赋给point


/*******************************************************************************
 * 流程控制
 ******************************************************************************/
// for
i := 10
for i > 0 {
    println(i--)
}
// if else
if i == 10 {
    println("i == 10")
} else {
    println("i != 10")
}
// switch
switch i {
case 10:
    println("i == 10")
default:
    println("i != 10")
}


/*******************************************************************************
 * 函数
 ******************************************************************************/
// 以func关键字声明
func test() {}

f := func() {println("Lambdas function")}     // 匿名函数
f()

func get() (a,b string) {                    // 函数多返回值
    return "a", "b"
}
a, b := get()




/*******************************************************************************
 * 结构体
 ******************************************************************************/
// golang中没有class只有struct
type People struct {
  Age int                                  // 大写开头的变量在包外可以访问
  name string                              // 小写开头的变量仅可在本包内访问
}
p1 := People{25, "Kaven"}                 // 必须按照结构体内部定义的顺序
p2 := People{name: "Kaven", age: 25}      // 若不按顺序则需要指定字段

// 也可以先不赋值
p3 := new(People)
p3.Age = 25
p3.name = "Kaven"


/*******************************************************************************
 * 方法
 ******************************************************************************/
// 方法通常是针对一个结构体来说的
type Foo struct {
  a int
}
                                        // 值接收者
func (f Foo) test() {
  f.a = 1                              // 不会改变原来的值
}
                                      // 指针接收者
func (f *Foo) test() {
  f.a = 1                            // 会改变原值
}



/*******************************************************************************
 * go 协程
 ******************************************************************************/
go func() {
    time.Sleep(10 * time.Second)
    println("hello")
}()                                // 不会阻塞代码的运行 代码会直接向下运行
// channel 通道
c := make(chan int)
// 两个协程间可以通过chan通信
go func() {c <- 1}()              // 此时c会被阻塞 直到值被取走前都不可在塞入新值
go func() {println(<-c)}()
// 带缓存的channel
bc := make(chan int, 2)
go func() {c <- 1; c <-2}()      // c中可以存储声明时所定义的缓存大小的数据，这里是2个
go func() {println(<-c)}()



/*******************************************************************************
 * 接口
 ******************************************************************************/
// go的接口为鸭子类型，即只要你实现了接口中的方法就实现了该接口
type Reader interface {
    Reading()                  // 仅需实现Reading方法就实现了该接口
}

type As struct {}
func (a As) Reading() {}      // 实现了Reader接口

type Bs struct {}
func (b Bs) Reading() {}      // 也实现了Reader接口
func (b Bs) Closing() {}




/*******************************************************************************
 * 一些推荐
 ******************************************************************************/
// 入门书籍
《Go学习笔记》                // 雨痕的
《Go语言实战》                // 强烈推荐
// 网上资料
https://github.com/astaxie/build-web-application-with-golang    // 谢大的
https://github.com/Unknwon/the-way-to-go_ZH_CN                  // 无闻
https://github.com/Unknwon/go-fundamental-programming           // 无闻教学视频
// 第三方类库
https://golanglibs.com/
// 大杂烩
https://github.com/avelino/awesome-go
```





# Linux

## 命令

```css
uptime 当前时间、系统运行了多久时间、当前登录的用户有多少，以及前 1、5 和 15 分钟系统的平均负载。
uptime -p 系统运行了多长小时和分钟
uptime -s 系统开始运行的时间

文件传输
bye、ftp、ftpcount、ftpshut、ftpwho、ncftp、tftp、uucico、uucp、uupick、uuto、scp

备份压缩
ar、bunzip2、bzip2、bzip2recover、compress、cpio、dump、gunzip、gzexe、gzip、lha、restore、tar、unarj、unzip、zip、zipinfo

文件管理
diff、diffstat、file、find、git、gitview、ln、locate、lsattr、mattrib、mc、mcopy、mdel、mdir、mktemp、mmove、mread、mren、mshowfat、mtools、mtoolstest、mv、od、paste、patch、rcp、rhmask、rm、slocate、split、tee、tmpwatch、touch、umask、whereis、which、cat、chattr、chgrp、chmod、chown、cksum、cmp、cp、cut、indent

磁盘管理
cd、df、dirs、du、edquota、eject、lndir、ls、mcd、mdeltree、mdu、mkdir、mlabel、mmd、mmount、mrd、mzip、pwd、quota、quotacheck、quotaoff、quotaon、repquota、rmdir、rmt、stat、tree、umount

磁盘维护
badblocks、cfdisk、dd、e2fsck、ext2ed、fdisk、fsck.ext2、fsck、fsck.minix、fsconf、hdparm、losetup、mbadblocks、mformat、mkbootdisk、mkdosfs、mke2fs、mkfs.ext2、mkfs、mkfs.minix、mkfs.msdos、mkinitrd、mkisofs、mkswap、mpartition、sfdisk、swapoff、swapon、symlinks、sync

系统设置
alias、apmd、aumix、bind、chkconfig、chroot、clock、crontab、declare、depmod、dircolors、dmesg、enable、eval、export、fbset、grpconv、grpunconv、hwclock、insmod、kbdconfig、lilo、liloconfig、lsmod、minfo、mkkickstart、modinfo、modprobe、mouseconfig、ntsysv、passwd、pwconv、pwunconv、rdate、resize、rmmod、rpm、set、setconsole、setenv、setup、sndconfig、SVGAText Mode、timeconfig、ulimit、unalias、unset

系统管理
adduser、chfn、chsh、date、exit、finger、free、fwhois、gitps、groupdel、groupmod、halt、id、kill、last、lastb、login、logname、logout、logrotate、newgrp、nice、procinfo、ps、pstree、reboot、renice、rlogin、rsh、rwho、screen、shutdown、sliplogin、su、sudo、suspend、swatch、tload、top、uname、useradd、userconf、userdel、usermod、vlock、w、who、whoami、whois

文本处理
awk、col、colrm、comm、csplit、ed、egrep、ex、fgrep、fmt、fold、grep、ispell、jed、joe、join、look、mtype、pico、rgrep、sed、sort、spell、tr、uniq、vi、wc

网络通讯
dip、getty、mingetty、ppp-off、smbd(samba daemon)、telnet、uulog、uustat、uux、cu、dnsconf、efax、httpd、ifconfig、mesg、minicom、nc、netconf、netconfig、netstat、ping、pppstats、samba、setserial、shapecfg(shaper configuration)、smbd(samba daemon)、statserial(status ofserial port)、talk、tcpdump、testparm(test parameter)、traceroute、tty(teletypewriter)、uuname、wall(write all)、write、ytalk、arpwatch、apachectl、smbclient(samba client)、pppsetup

设备管理
dumpkeys、loadkeys、MAKEDEV、rdev、setleds

电子邮件与新闻组
archive、ctlinnd、elm、getlist、inncheck、mail、mailconf、mailq、messages、metamail、mutt、nntpget、pine、slrn、X WINDOWS SYSTEM、reconfig、startx(start X Window)、Xconfigurator、XF86Setup、xlsatoms、xlsclients、xlsfonts
```

# Lua