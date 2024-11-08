---
title: QT210 Android4.0源码编译和烧录
author: Leo
layout: post
category : programme
permalink:  /android-qt210-compile/
tags: 
  - android
  - qt210
  - system

---

# 开发环境说明：
- Ubuntu 12.04 LTS  32bit


# 源码文件目录：
- 勤研光盘2013-5-4\4.0
- [https://github.com/jackyh](https://github.com/jackyh) `（建议在Linux环境下通过git下载）`



# 编译过程说明
## 编译uboot  (qt210_ics_uboot.bz2)

交叉编译环境：
```shell	
tar jxf arm-2009q3-67-arm-none-linux-gnueabi-i686-pc-linux-gnu.tar.bz2 -C /usr/local/arm
```
注：必须解压到/usr/local/arm目录下，因为Android源码Makefile当中，包含了arm-linux-gcc的绝对路径。

然后进入到交叉编译压缩包的目录执行：
```shell
cd ./qt210_ics_uboot
make smdkv210single_config
make （编译）
```

完成后qt210_ics_uboot 目录下就有了u-boot.bin 文件，
qt210_ics_uboot/tools 目录中有了mkimage 文件(这个用来make uImage 的)
把mkimage所在的目录加入到环境变量中或者是把mkimage复制到/usr/bin目录中。

## 编译Kernel (qt210_ics_kernel.bz2)
```shell
cd qt210_ics_kernel3.0.8/	
cp config_capacity .config	
make -j2 uImage #–j4 也行，数字指参与编译的线程数
```
编译完成之后，在目录qt210_ics_kernel3.0.8/arch/arm/boot 中应该有uImage文件。
   
## 编译android（android_qt210.bz2）
在编译Android源码之前，一定要将开发环境搭建完成。比如：安装java6，gcc4.5等

**运行 qt210中包含的shell脚本：**
```shell
./installtools.sh
```

如果出现如下错误，将出错的项目从installtools.sh中去掉。再安装！
```
leo@teacher-A:~/qt210$ sh source/installtools.sh
get host tools now
正在读取软件包列表... 完成
正在分析软件包的依赖关系树       
正在读取状态信息... 完成       
E: 未发现软件包 libc6-dev-i386
E: 未发现软件包 ia32-libs
E: 未发现软件包 lib32z-dev
E: 未发现软件包 lib32ncurses5-dev
```

尽量的保证installtools.sh当中的软件都安装完成

**解压android源码：**
```shell
tar jxf android_qt210.tar.bz2
```

**运行qt210当中的shell脚本：**
```shell	
./compilesrc.sh #compilesrc.sh和解压后的android源码放在同一级目录
```

如果在编译过程当中出现缺少库的情况，那么缺什么库就安装什么库。

**编译** \
compilesrc.sh中的内容也比较简单，就是编译android源码的三个步骤：
```shell
source build/envsetup.sh
lunch full_smdkv210-eng
make -j4
```


## 烧写过程说明
**制作TF启动，也就是把UBOOT烧到TF卡中** \
将读卡器插入到电脑上在ubuntu虚拟机下,找到已经编译好的uboot所在文件夹。
```shell
cd qt210_ics_uboot/sd_fusing
sudo ./sd_fusing_uboot.sh /dev/sdb #将编译好的uboot烧录到tf卡当中
```

**将TF卡插入开发板，选择TF卡启动** \
进入bootloader模式，然后敲：
```shell	
fdisk -c 0 #格式化sd卡
fastboot #启动fastboot工具，使用fastboot需要连接USB OTG线
```

**在windows当中，建立文件夹将编译好的** \
u-boot.bin、uImage、ramdisk-uboot.img、system.img放入其中将fastboot.exe和leo_android.bat拷贝到目录当中leo_android.bat内容如下：
```
fastboot.exe flash bootloader u-boot.bin 
fastboot.exe flash kernel uImage 
fastboot.exe flash system system.img
fastboot.exe flash ramdisk ramdisk-uboot.img 
fastboot.exe -w
```

双击运行leo_android.bat,现在就通过fastboot协议烧录android系统 \
**烧录完成后将tf卡取出插入电脑在ubuntu下，清除第三分区**
```shell
sudo mkfs.ext4 /dev/sdb3
```

**插入开发板重启启动即可！**


## 注意
- 由于开发板android4.0.4移植的不够完善,有时候会出现电容屏不好使，或者无法解锁，所以，设置--developer options-->Stay awake
- 还有屏保时间设置最长为30min