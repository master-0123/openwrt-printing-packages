#
# Copyright (C) 2013 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=epson-inkjet-printer-escpr
PKG_VERSION:=1.8.6
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
#PKG_SOURCE_URL:=https://download.ebz.epson.net/dsc/du/02/DriverDownloadInfo.do?LG2=JA&CN2=US&CTI=176&PRN=Linux%20src%20package&OSC=LX&DL
#PKG_HASH:=skip

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PATCH_DIR:=./patches

include $(INCLUDE_DIR)/package.mk

define Package/epson-inkjet-printer-escpr
	SECTION:=net
	CATEGORY:=Network
	TITLE:=Epson Inkjet Printer Driver (ESC/P-R)
	URL:=https://www.epson.com/
	DEPENDS:=+cups
	SUBMENU:=Printing
endef
 
define Package/epson-inkjet-printer-escpr/description
	Epson Inkjet Printer Driver (ESC/P-R) for Linux, providing CUPS filters and PPD files for Epson printers.
endef

define Build/Prepare
	# 创建构建目录
	mkdir -p $(PKG_BUILD_DIR)
	# 手动下载源码到 dl/ 目录，使用 PKG_SOURCE 指定的文件名
	@echo "Downloading $(PKG_NAME) source..."
	@if [ ! -f $(DL_DIR)/$(PKG_SOURCE) ]; then \
		curl -f -o $(DL_DIR)/$(PKG_SOURCE) \
			--connect-timeout 20 --retry 5 \
			-A "Mozilla/5.0" \
			https://download3.ebz.epson.com.cn/dsc/f/03/00/16/21/81/74d098a47c3a616713079c9cd5904b468bb33dea/epson-inkjet-printer-escpr-1.8.6-1.tar.gz || \
		( echo "Download failed"; rm -f $(DL_DIR)/$(PKG_SOURCE); exit 1 ); \
	else \
		echo "Using existing $(DL_DIR)/$(PKG_SOURCE)"; \
	fi

	@echo "Extracting $(PKG_SOURCE)..."
	tar -xzf $(DL_DIR)/$(PKG_SOURCE) -C $(PKG_BUILD_DIR) || exit 1
	
	@echo "Adjusting directory structure..."
	@if [ -d "$(PKG_BUILD_DIR)/epson-inkjet-printer-escpr-1.8.6" ]; then \
		mv $(PKG_BUILD_DIR)/epson-inkjet-printer-escpr-1.8.6/* $(PKG_BUILD_DIR)/ && \
		rmdir $(PKG_BUILD_DIR)/epson-inkjet-printer-escpr-1.8.6; \
	elif [ -d "$(PKG_BUILD_DIR)/epson-inkjet-printer-escpr-1.8.6-1" ]; then \
		mv $(PKG_BUILD_DIR)/epson-inkjet-printer-escpr-1.8.6-1/* $(PKG_BUILD_DIR)/ && \
		rmdir $(PKG_BUILD_DIR)/epson-inkjet-printer-escpr-1.8.6-1; \
	else \
		echo "Warning: Unexpected directory structure after extraction."; \
	fi

	$(call PatchDir,$(PKG_BUILD_DIR),$(PATCH_DIR))
endef

# 配置编译选项
CONFIGURE_ARGS += \
	--with-cupsfilterdir=$(1)/usr/lib/cups/filter \
	--with-cupsppddir=$(1)/usr/share/cups/model

define Build/Configure
	$(call Build/Configure/Default)
endef

define Build/Compile
	$(call Build/Compile/Default)
endef

define Package/epson-inkjet-printer-escpr/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_DIR) $(1)/usr/share/cups/model
	$(INSTALL_DIR) $(1)/usr/lib/cups/filter
	$(MAKE) -C $(PKG_BUILD_DIR) DESTDIR=$(1) install

	# 压缩 PPD 文件
	find $(1)/usr/share/cups/model -name "*.ppd" -exec gzip -9 -f {} \;
endef

define Package/postinst
#!/bin/sh
/etc/init.d/cupsd stop
/etc/init.d/cupsd start
endef

$(eval $(call BuildPackage,epson-inkjet-printer-escpr))
