---
layout: post
title:  TcpReplay的安装
date:   2016-11-25 
category: "学习"
---
<h2 id="tagline">TcpReplay--回放工具</h2>



<h2 id="section1">一、TcpReplay</h2>
<p> Tcpreplay是一系列工具的总称，包括tcpreplay、tcprewrite和tcpprep等工具.</p>
<ol>
    <li>tcpprep：这个工具的作用就是划分客户端和服务器，区分pcap数据包的流向，即划分那些包是client的，哪些包是server的，一会发包的时候client包从一个网卡发，另一个server的包可能从另一个网卡发。</li>
    <li>tcprewrite：这个工具的作用就是来修改报文，主要修改2层，3层，4层报文头，即MAC地址，IP地址和PORT地址。</li>
    <li>tcpreplay：这是最终真正发包使用的工具，可以选择主网卡、从网卡、发包速度等。</li>
</ol>


<h2 id="section2"> 二、TcpReplay安装过程</h2>
<p> 第一步，安装一个linux系统；第二步，安装tcpreplay以及相关组件.</p>
<ol>
    <li>安装libpcap库（在安装tcpreplay之前需要先安装libpcap），安装libpcap之前需要首先安装m4、bison flex，否则会出现错误
        <ol>
            <li>1）：打开网址：<a href="http://www.tcpdump.org/release/">http://www.tcpdump.org/release/</a> 下载 libpcap-1.1.1.tar.gz (512.0KB) 软件包，通过命令tar zxvf libpcap-1.1.1.tar.gz 解压文件，并将其放入自定义的安装目录。</li>
            <li>2）：打开网址：<a href="https://sourceforge.net/projects/flex/files/">https://sourceforge.net/projects/flex/files/</a> 下载 flex-2.5.35.tar.gz (1.40MB) 软件包，通过 tar zxvf flex-2.5.35.tar.gz  解压文件，并将其放入上述自定义的安装目录中。<br />
                     注意：如果没有编译安装此文件，在编译安装libpcap时，就会出现 “configure: error: Your operating system\'s lex is insufficient to compile libpcap.”的错误提示。</li>
            <li>3）：打开网址：<a href="https://ftp.gnu.org/gnu/bison/">https://ftp.gnu.org/gnu/bison/</a> 下载 bison-2.4.1.tar.gz (1.9MB) 软件包，通过 tar zxvf bison-2.4.1.tar.gz 解压文件，并将其放入上述自定义的安装目录中。<br />
                     注意：如果没有编译安装此文件，在编译安装libpcap时，就会出现 "configure: WARNING: don\'t have both flex and bison; reverting to lex/yacc checking for capable lex... insufficient" 的错误提示。</li>
            <li>4）：打开网址：<a href="https://ftp.gnu.org/gnu/m4/">https://ftp.gnu.org/gnu/m4/</a>  下载 m4-1.4.13.tar.gz (1.2MB)软件包，通过 tar zxvfm4-1.4.13.tar.gz 解压文件，并将其放入上述自定义的安装目录中。<br />
         注意：如果没有编译安装此文件，在编译安装bison-2.4.1时，就会出现 “configure: error: GNU M4 1.4 is required”的错误示。<br />
         然后，依次进入（注意顺序）m4-1.4.13，bison-2.4.1，flex-2.5.35，libpcap-1.1.1 并执行以下命令：<br />
         # ./configure <br />
         # make  <br />
         # make install  <br />
         命令完成后，libpcap才能正常使用。</li>
        </ol>
    </li>
    <li>安装完libpcap后就可以安装tcpreplay了<br />
    从这个链接<a href="http://tcpreplay.synfin.net/wiki/Download">http://tcpreplay.synfin.net/wiki/Download</a>下载tcpreplay-4.1.2.tar.gz软件包，通过 tar zxvf tcpreplay-4.1.2.tar.gz  解压文件，并将其放入上述自定义的安装目录中。然后进入tcpreplay-4.1.2，并执行以下命令：<br />
    # ./configure <br />
    # make  <br />
    # make install  <br />
    注意安装tcpreplay时一般会出现以下错误：<br />
    "checking for libpcap version... configure: error: Libpcap versions &lt 0.7.2 are not supported Please upgrade to version 0.7.2 or better" <br />
    这是因为configure中是这样判断libpcap版本的：<br />
    if test $libpcap_ver8 = yes ; then <br />
      { $as_echo "$as_me:$LINENO: result: >= 0.8.0" > &amp 5  <br />
    $as_echo ">= 0.8.0" >&6; }  <br />
    elif test $libpcap_ver7 = yes ; then   <br />
     { $as_echo "$as_me:$LINENO: result: >= 0.7.2" > &amp 5   <br />
    $as_echo ">= 0.7.2" >&6; }   <br />
    else  <br />
      { { $as_echo "$as_me:$LINENO: error: Libpcap versions &lt 0.7.2 are not supported  <br />
    Please upgrade to version 0.7.2 or better" > &amp 5    <br />
    我装的libpcap是1.1.1版本的，肯定符合要求，所以将这段代码注释掉。<br />
    执行完后，tcpreplay 就可以使用了，可以通过命令：tcpreplay –vesion来查看它的版本信息，tcpreplay –h来查看帮助内容。</li>
</ol>

