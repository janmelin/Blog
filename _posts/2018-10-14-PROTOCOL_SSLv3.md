---
layout: post
title: NameError: name 'PROTOCOL_SSLv3' is not defined
---


今天把Mac升级到10.14系统后，某python程序立即报错。这是一个别人多年前的项目。程序早已不再更新，但十分好用，于是延用至今。

python报错如下：
`NameError: name 'PROTOCOL_SSLv3' is not defined`

这个问题不太难，go一下就能找到解决方法。就是将`PROTOCOL_SSLv3`改为`PROTOCOL_SSLv23`。
>the default ssl\_version is changed from PROTOCOL\_SSLv3 to PROTOCOL\_SSLv23 for maximum compatibility with modern servers.

不过真正的难点并不在这里，而是在于如何修改。

这个py文件是打包在egg文件中的。egg是个“zip”文件，所以先尝试了“zip解压缩-修改-zip压缩”的方式。然而自己压缩的egg(zip)文件不能被相关程序读取（估计是因为egg是无压缩的zip且含有其他信息），之后也尝试“不打包+修改源代码”，“zip解压缩-修改-egg生成”，但都未能成功。前者是由于需要修改工作量过大而作罢，后者则是由于解压出来的文件不含有egg生成必须的文件，而自己从头学写\_\_init.py\_\_同样也很麻烦。

后来灵机一动，想起能否直接用修改过的文件替换zip中的文件。go了一下，发现vim可以直接打开并修改zip文件，于是问题得到解决。
