# Brook

[TOC]

## Linux Server



## Windows client

Windows客户端有两种版本：cmd命令行和gui图形界面，不过我更喜欢使用cmd命令行版本

**步骤：**

- 从github上下载brook_windows_amd64.exe，在C盘创建brook文件夹，拷贝到 C:\brook 文件夹下

- 文件夹内需要新建以下三个文件 

  > brook_windows_amd64.exe

  > brook-scripts-http-proxy.bat

  > startBrook.vbs

  ```
  C:\brook>dir
   驱动器 C 中的卷没有标签。
   卷的序列号是 722E-468E
  
   C:\brook 的目录
  
  2019/04/26  08:34    <DIR>          .
  2019/04/26  08:34    <DIR>          ..
  2019/04/26  08:26               114 brook-scripts-http-proxy.bat
  2019/04/26  07:51        13,268,480 brook_windows_amd64.exe
  2019/04/26  08:41                91 startBrook.vbs
                 3 个文件     13,268,685 字节
                 2 个目录 62,332,370,944 可用字节
  ```

- 编写`brook-scripts-http-proxy.bat`的内容

  github上关于windows客户端启动brook的两种方式

  ```
  # Run as brook client, start a socks5 proxy socks5://127.0.0.1:1080
  $ brook client -l 127.0.0.1:1080 -i 127.0.0.1 -s server_address:port -p password
  
  # Run as brook client, start a http(s) proxy http(s)://127.0.0.1:8080
  $ brook client -l 127.0.0.1:8080 -i 127.0.0.1 -s server_address:port -p password --http
  ```

  以下是现在使用的`brook-scripts-http-proxy.bat`范例，建议使用http，更方便配置

  ```
  C:\brook\brook_windows_amd64.exe client -l 127.0.0.1:1080 -i 127.0.0.1 -s 103.124.104.21:33456 -p ntdtv.com --http
  ```

- 编写`startBrook.vbs`内容

  ```
  Set ws = CreateObject("Wscript.Shell")
  ws.run "cmd /c brook-scripts-http-proxy.bat",vbhide
  ```

- 打开IE浏览器，依次点击“设置”->"Internet选项"->“连接”->"局域网设置"->"代理服务器"->"为LAN使用代理服务器"，配置`地址 127.0.0.1 端口 1080`，即可浏览器全局代理
- 如果需要设置部分代理，可以使用两个浏览器，例如google浏览器默认浏览网页，即可全局代理，firefox设置不使用代理，即可无代理。
- 如果需要关闭脚本，可以打开“任务管理器”，手动关闭“Windows 命令处理程序”，即可。
