[**[中文]**](README.md) [**[English]**](README-en.md)
# OpenWrt Printing Software Packages
 
Includes:
 
- Cups 2.4.12 5MB  
  Linux Universal Printing Service
- foo2zjs 20200505dfsg0-3 1.3MB  
  Driver for Classic HP 1XXX Printers
- foo2zjs-extra 11.8MB  
  Firmware and ICC files for Classic HP 1XXX Printers; you can extract and only copy the files you need^[1]^
- Gutenprint 5.3.5 4.9MB  
  Open-source print driver, supports a wide range of printer models
- Epson-inkjet-printer-escpr 1.8.6 4.8MB  
  Driver for Epson Inkjet Printers
- OpenPrinting's cups-filters 2.0.1 146kB  
  CUPS Filters, many open-source print drivers depend on them; the CUPS test page is included in this package^[2]^
- libcupsfilters 2.1.1 524kB  
  Library files for OP-cups-filters
- libppd 2.1.1 201kB  
  Library files for OP-cups-filters
- Ghostscript 10.04.0 21.9MB  
  PDF processing software, many open-source print drivers depend on it
- ghostscript-fonts-std 3.8MB
- lcms2 2.17 375kB
- Cairo 1.18.4
- libjbigkit 2.1
- poppler 0.90.0
- qpdf 12.2.0

## 📌 How to Compile?
 
### Method 1:
 
Before executing `./scripts/feeds update -a`, insert the following code at the **top** of `feeds.conf.default`:

```
src-git printing-packages https://gitee.com/master0123/openwrt-printing-packages.git;master
```

### Method 2:
 
After executing `./scripts/feeds install -a`, run the following command:

```shell
git clone --depth=1 https://github.com/master-0123/openwrt-printing-packages package/printing-packages
```

### Note:

To compile Ghostscript, the host system must have the cups and libcups2-dev packages installed.
The above software packages have not undergone rigorous testing. Please use them with caution.

--------------------------------------------

Acknowledgments

https://github.com/SoPudge/lede-cups

https://github.com/obanat/openwrt-printing-packages

https://github.com/mengtw123/openwrt-printing-packages

https://github.com/jastheace/openwrt-printing-packages
