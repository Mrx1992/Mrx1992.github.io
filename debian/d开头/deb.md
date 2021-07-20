# deb

[官方手册](https://manpages.debian.org/buster/dpkg-dev/deb.5.en.html)

## 名字

deb：Debian二进制包格式

## 大纲

包名.deb

## 描述

`.deb`这种格式是debian二进制包的格式。他是从dpkg0.93.76开始被理解，从dpkg 1.2.0和1.1.1elf（i386/ELF构建）开始默认生成的。

这里描述的格式是从Debian 0.93开始使用的；旧格式的细节在[deb-old](deb-old)中描述。

## 格式

这个文件是一个ar存档，具有一个神奇的值`!<arch>`。只支持普通的ar档案格式，不包含长文件名扩展，但是文件名可以包含一个反斜杠，这样长度限制将为15个字符（原本允许16个）。文件大小限制在10个ascII十进制数字，

允许最多约9536.74MB的成员文件。