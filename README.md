# Printing packages for OpenWrt

OpenWrt上的打印软件包移植，包括：

- Cups 2.4.12							  5MB
  Linux通用打印服务
- foo2zjs 20200505dfsg0-3				  1.3MB
  HP 1XXX等经典打印机驱动
- foo2zjs-extra							 11.8MB
  HP 1XXX等经典打印机固件和ICC文件，可以解压后仅复制自己需要的文件
- Gutenprint 5.3.5						   4.9MB
  开源打印驱动，支持打印机型号众多
- Epson-inkjet-printer-escpr 1.8.6  		4.8MB
  Epson喷墨打印机驱动
- OpenPrinting's cups-filters 2.0.1			146kB
  CUPS过滤器，很多开源打印驱动依赖，Cups的测试页面在这个包里
- libcupsfilters 2.1.1						524kB
  OP-cups-filters的库文件
- libppd 2.1.1								201kB
  OP-cups-filters的库文件
- Ghostscript 10.04.0    					21.9MB
  PDF处理软件， 很多开源打印驱动依赖
- ghostscript-fonts-std    					 3.8MB
- lcms2 2.17 								375kB
- Cairo 1.17.4
- libjbigkit 2.1
- libpcre 8.41
- poppler 0.90.0
- qpdf 12.2.0
- hplip 3.18.6
  HP官方打印机驱动，最后一个能自编译支持全平台的驱动，后期版本内prnt/libImageProcessor.so只有x86和arm二进制文件，不开源；安装后还需要安装hplip-3.18.6-plugin，这个里面只有x86和arm的二进制文件，需要python支持，太麻烦懒得测试了


git clone --depth=1 https://github.com/xiaorouji/openwrt-printing-packages package/openwrt-printing-packages
以上软件包未经严谨测试，请谨慎使用。

--------------------------------------------
致谢
https://github.com/SoPudge/lede-cups
https://github.com/obanat/openwrt-printing-packages
https://github.com/mengtw123/openwrt-printing-packages
https://github.com/jastheace/openwrt-printing-packages