# Getitle
一个资产探测扫描器. 

README Version 1.2.0

## Usage

```
Usage of ./getitle:

   -k string   key,启动密码(必须输入) 
   -debug bool  输出每个请求的错误日志, 用来debug
   
   INPUT params:
      -ip string   IP地址, 支持逗号分割的输入 like 192.168.1.1/24,172.16.1.1/24
      -eip string exclude_ip, 排除指定的ip地址,支持cidr, 支持逗号分割 -eip 192.168.1.1/28,192.168.1.199 
      -p string   ports, (default "top1")
         default 非特殊指定其他端口, 均默认使用这种方式扫描, 使用socket发送GET包
         nbt  使用netbios收集域,sharing,DC信息
         oxid 使用wmi协议收集网卡信息
         smb  使用ntlm协议收集主机名/域信息
         wmi 使用wmi的ntlm协议收集信息,与smb的协议收集到的内容一致 
         snmp 使用snmp public收集信息
         icmp/ping 使用ping判断存活
         arp 使用arp协议判断ip存活, 并收集mac地址
         winrm 不太常用,暂时删除

      -m string  mod, 扫描模式：(每次只能选择一个生效)
            default (默认值, 资产扫描),
            s B段启发式扫描,
            ss A段启发式扫描
            sc 以ss模式发现所有存活C段(但不会进行端口扫描)
            a 根据默认配置自动启发式扫描
      -l string  listfile, 从文件中读取任务,例如:-l ip.txt
      -j string	 jsonfile, 从输出的json中读取任务,例如:-j 1.json
      -L bool    List_File_From_Pipe , 从管道中读数据的时候,指定数据类型为行分割的数据
      -J bool    Json_File_From_Pipe 从管道中读数据的时候, 指定数据为前一次的扫描结果, 从传入管道前请base64, 否则可能因为EOF字符被截断
      -F file    Format, 格式化扫描结果
      -w string  workflow, 调用自动化配置的预设  
      
   SMART CONFIGS
      -sp string  smart_probe,启发式扫描端口探针,-m s 下默认为80, -m ss下默认为icmp
      -ipp string smart_ip_probe, -ss模式ip探针,默认1
      -no bool	  noscan,   (依赖-m s/ss) 高级扫描模式只探测存活网段不进行端口扫描
      -ping bool  pingscan, 在端口扫描前插入一次ping 喷洒, 存活的ip才会被加入端口扫描.
 
   OUTPUT params:
      -o string  output,  输出到命令行的格式:clean,full(default) or json, 以及ip, url, target, zombie(仅限-F), cs(仅限-F) 等多种输出格式
      -O string  FileOutput, 输出到文件的格式: clean, full, json(default) 以及ip, url, target
      -f string  file,  输出文件名,默认为空
      -path string 指定输出的目录, -f参数默认为当前目录, -af/hf参数为程序绝对目录
      -af bool	autofile,   自动生成文件名,格式为 ".IP_port_number.json"
      -hf bool  hiddenfile,   自动生成隐藏文件名.
      -C bool   Clear,   强制关闭输出文件压缩, 变成明文输出

      -c string    在指定了-f的情况下强制打开命令行输出扫描结果
      -q bool   quiet, 不在命令行输出进度日志
      -P string Print, 查看配置预设  port|nuclei|workflow|extract 
         port 端口预设
         nuclei 可以选用的poc
         workflow workflow预设
         extract  extract预设

   CONFIGURATIONS params:
      -version     输出版本号
      -d int     delay, 超时,默认2s (default 2)
      -D int     Https_Delay,  https协议单独配置的超时, 默认4s
      -s bool 	 spray,  喷洒模式扫描,ip生成器将端口为优先,端口数量大于100将自动启用
      -ns bool	 no_spray,  强制关闭spray扫描
      -t int     threads, (default 4000), windows下默认1000, fd限制为1024的linux下默认为900
      -v bool    version_scan, 扫描详细指纹.默认为打开状态,存在-v参数则关闭.
      -e bool    exploit_scan, 启用漏洞插件扫描,目前有ms17-010与shiro(默认key),以及nuclei的poc,将会自动选用
      -E string  Exp_name, 强制指定poc的tag或name, 指定-E all 时为全部poc
      -ef string exploit_file, 指定json文件为nucleipoc
      -up string upload_file,  指定文件上传到云服务器
      -np bool   no_upload, 关闭自动上传扫描结果到云服务器
      -suffix string 指定特定的url
      -payload 用来自定义替换nuclei poc中的参数, 需要nuclei poc预定义占位符
      -extract 自定义需要提取的内存, 输入正则表达式, 支持一些常见的预设
      -extracts 逗号分割的多个extractor预设
   ```

## 二进制文件下载链接

完全版本打包下载: https://github.com/ZTeam-H3/getitle/releases/latest

理论上支持全操作系统, 需要编译某些稍微罕见的特殊版本可以联系我帮忙编译.

单文件下载链接:

**windows**

[windows32upx](https://sangfor-release.oss-cn-shanghai.aliyuncs.com/fscan/windows_386_upxs.exe)
 [windows32](https://sangfor-release.oss-cn-shanghai.aliyuncs.com/fscan/windows_386s.exe)
 [windows64](https://sangfor-release.oss-cn-shanghai.aliyuncs.com/fscan/windows_amd64s.exe)
 [windows64upx](https://sangfor-release.oss-cn-shanghai.aliyuncs.com/fscan/windows_amd64_upxs.exe)

**linux**

[linux_amd64](https://sangfor-release.oss-cn-shanghai.aliyuncs.com/fscan/linux_amd64)
 [linux_amd32](https://sangfor-release.oss-cn-shanghai.aliyuncs.com/fscan/linux_386)
 [linux_arm64](https://sangfor-release.oss-cn-shanghai.aliyuncs.com/fscan/linux_arm64)
 [linux_mips64](https://sangfor-release.oss-cn-shanghai.aliyuncs.com/fscan/linux_mips64)

**mac**

[mac](https://sangfor-release.oss-cn-shanghai.aliyuncs.com/fscan/darwin_amd64)

## QuickStart
最简使用

`gt -k [key] -ip 192.168.1.1/24 -p win,db,top2 `

一行内网全冲

`gt -k [key] -w inter -e -v`

使用工作流, 启发式扫描10段常见端口

`gt -k [key] -w 10`

不适用工作流, 手动指定特定网段与配置

`gt -k [key] -ip 172.16.1.1/16 -m s -p all -e -v -af`

查看全部可用工作流

`gt -k [key] -P workflow`

### workflow
workflow 使用思维导图

![](doc/img/pipeline.png)

### 手动组合参数
参数使用较为复杂, 现在已经基本被淘汰, 仅在少数workflow没有覆盖的场景下手动指定

**喷洒存活C段**

`gt -k [key] -ip 172.16.0.0/16 -m s -no -af`

**喷洒存活B段**

`gt -k [key] -ip 10.0.0.0/8 -m ss -no -af`

**递归下降喷洒C段(在A段中喷洒C段)**

`gt -k [key] -ip 10.0.0.0/8 -m sc -af`

## 参数解释

所有用法都需输入-k [密钥]

### target输入

1. 直接输入cidr,参数-ip 1.1.1.1/24, 支持逗号分割
2. 从文件中读ip列表, 参数 -l 1.txt
3. 从结果中读任务列表,参数 -j 1.json
4. 从管道中读取列表, -L
5. 从管道中读取结果, -J

### 端口配置

gt支持非常灵活的端口配置

参看端口预设,参数 -P port

使用端口预设灵活配置端口: -p top2,http,1-1000,65534


### 输出

输出分为两大类,输出到文件或输出到命令行.在webshell场景下,通常无法输出到命令行.

#### 输出到命令行

默认即可输出到命令行,但是在选择输出到文件的时候会关闭命令行输出.此时可以使用-c手动开启

输出格式:clean,full(default) or json, 以及ip, url, target, zombie, cs 等多种输出格式

-q 参数关闭进度输出

#### 输出到文件

-f 参数指定输出文件

-af 自动生成文件名

-hf 自动生成隐藏文件名

-C 关闭输出到文件的压缩

-c 在输出到文件时, 仍然保留命令行输出

#### 格式化结果

-F 参数可以格式化JSON,拥有比full更加整洁与美化的输出结果.

还可以使用`-F 1.json -o c`来着色

也可以使用`-F 1.json -o ip` 来过滤出指定字段

### 启发式扫描配置

-m s 为喷洒C段模式,子网掩码要小于24才能使用

-m ss 为喷洒B段模式, 子网掩码要小于16才能使用

-m sc 为在A段中收集存活C段, 子网掩码要小于16才能使用

-no 只进行启发式扫描,在喷洒到网段后不进行全扫描. 可以配合-f参数将启发式扫描喷洒到的网段输出到文件.例如 `-s -no -f aliveC.txt`

-sp (smart probe)控制启发式扫描的探针,默认为icmp协议,可以手动指定为其他配置,例如`-sp 80,icmp,445 ` 来在禁ping的环境下使用

-ipp (IP probe) 控制-ss模式中的B段喷洒的ip探针,-ss模式默认只扫描每个C段的第一个ip,例如192.168.1.1. 可以手动修改,指定`-ipp 1,254,253`

### 其他配置

-t 设置线程数,linux默认4000,windows默认20000

-d tcp与http协议的超时时间,默认2s

-D 单独指定https协议的超时时间,默认4s

-s 为端口的spray模式,打开后将使用同一个端口与每个IP组合,防止同一个IP的请求过多造成漏报. 此参数支持-l 从文件中输入

-v 会进行主动发包的指纹探测

-e 进行漏洞探测,目前只是个demo,未来将会支持xray,goby的poc


## 使用场景



**格式化json输出**

`./gt.exe -F out.txt`

启发式扫描只会先扫描80端口,如果在该C段中扫描到了80端口,则进行已配置端口的完整扫描.加快扫描速度.


`./gt.exe -ip 172.16.1.1/24 -p top2,db,mail,jboss,1000-1009,12345,54321`

**端口Spray模式**

任务生成器会以端口优先生成任务

`./gt.exe -ip 172.16.1.1/24 -p top2 -s`

**指纹识别**

当前包括数千条web指纹, 数百条favicon指纹以及数十条tcp指纹

默认情况下只收集不主动发包的指纹. 如需进行主动的指纹识别, 需要添加-v参数.

`./gt.exe -ip 192.168.1.1/24 -p top2 -v `

**漏洞探测**

getitle并非漏扫工具,因此不会支持sql注入,xss之类的通用漏洞探测功能.

为了支持内网更好的自动化, 集成了nuclei的poc, 可以用来编写poc批量执行某些特定的扫描任务, 一级一些默认口令登录的poc

因为nuclei的中poc往往攻击性比较强, 因此需要手动修改适应红队环境

目前已集成的pocs见v1/config/nuclei, 以及ms17010, shiro, snmp等特殊的漏洞

使用:

`./gt.exe -ip 192.168.1.1/24 -p top2 -v -e`

**高级启发式扫描**

[见getitle设计文档3-启发式扫描](doc/getitle设计文档3-启发式扫描.md)


**特殊扫描端口**

WMI
`./gt.exe -ip 172.16.1.1/24 -p wmi`

OXID:

`./gt.exe -ip 172.16.1.1/24 -p oxid`

NBTScan

`./gt.exe -ip 172.16.1.1/24 -p nbt`

PING

`./gt.exe -ip 172.16.1.1/24 -p icmp`

snmp

`./gt.exe -ip 172.16.1.1/24 -p snmp`

SMB
`./gt.exe -ip 172.16.1.1/24 -p smb`

可以任意组合使用,例如:
`./gt.exe -ip 172.16.1.1/24 -p smb,wmi,oxid,nbt,icmp,80,443,top2`

## 注意事项

* **(重要)**因为并发过高,性能限制主要来自路由器设备.因此**建议在阿里云,华为云等vps上使用**,如果扫描国外资产,建议在国外vps上使用.本地使用如果网络设备性能不佳会带来大量丢包.

* 如果使用中发现疯狂报错,大概率是io问题(例如多次扫描后io没有被正确释放,或者配合proxifier以及类似代理工具使用报错),可以通过重启电脑,或者虚拟机中使用,关闭代理工具解决.如果依旧无法解决请联系我们.

* 还需要注意,upx压缩后的版本虽然体积小,但是有可能被杀软杀,也有可能在部分机器上无法运行.

* 一般情况下无法在代理环境中使用,除非使用-t参数指定较低的速率(默认协程池为4000).

### 使用场景并发推荐
使用-t参数手动指定并发

* 家用路由器(例如钓鱼, 物理, 本机扫描)时, 建议并发 100-500
* linux 生产网网络环境(例如外网突破web获取的点), 默认并发4000, 不需要手动修改 
* windows 生产网网络环境, 默认并发1000, 不需要手动修改
* 高并发下udp协议漏报较多, 例如获取netbois信息时, 建议单独对udp重新探测
* web的正向代理(例如regeorg),建议并发 10-50
* 反向代理(例如frp), 建议并发10-100

如果如果发生大量漏报的情况, 大概率是网络环境发生的阻塞, 倒是网络延迟上升超过上限.

因此也可以通过`-d 5 `(tcp默认为2s, tls为两倍tcp超时时间4s)来提高超时时间, 减少漏报.

## Make

### make.bat:
需要依赖gox

`go get github.com/mitchellh/gox`

可以带两个参数, 第一个为版本号, 第二个为key, 不加则自动为空

`make.bat [key]`


### obfuscate.bat
发布前一些简单的混淆, 有更高明的手段可以忽略这部分

使用go-strip 混淆函数名, 使用upx加壳, 使用limelighter伪造证书. 需要将这三个工具添加到环境变量.

### release.bat 
自动将单个文件上传到alioss, 将README.md 二进制文件和一些小工具打包.

### full

`./make.bat [key] ; ./obfuscate.bat ; release.bat `

## THANKS

* https://github.com/k8gege/LadonGo
* https://github.com/projectdiscovery/nuclei-templates
* https://github.com/projectdiscovery/nuclei
* https://github.com/JKme/cube
    