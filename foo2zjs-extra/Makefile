#
# Copyright (C) 2013 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=foo2zjs-extra
PKG_VERSION:=1.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).zip
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PATCH_DIR:=./patches

include $(INCLUDE_DIR)/package.mk

define Package/foo2zjs-extra
	SECTION:=net
	CATEGORY:=Network
	TITLE:=Extra files for foo2zjs (All ICC files and firmwares)
	URL:=https://github.com/koenkooi/foo2zjs
	DEPENDS:=+foo2zjs
	SUBMENU:=Printing
endef

define Package/foo2zjs-extra/description
	Extra files for foo2zjs (All ICC files and firmwares)
endef

define Build/Prepare
	# 创建构建目录
	mkdir -p $(PKG_BUILD_DIR)
	# 手动下载源码到 dl/ 目录，使用 PKG_SOURCE 指定的文件名
	@echo "Downloading foo2zjs-extra source..."
	@if [ ! -f $(DL_DIR)/$(PKG_SOURCE) ]; then \
		curl -f -o $(DL_DIR)/$(PKG_SOURCE) \
			--connect-timeout 20 --retry 5 \
			https://github.com/koenkooi/foo2zjs/archive/master.zip || \
		( echo "Download failed"; rm -f $(DL_DIR)/$(PKG_SOURCE); exit 1 ); \
	else \
		echo "Using existing $(DL_DIR)/$(PKG_SOURCE)"; \
	fi
	# 解压到构建目录
	unzip -q -d $(PKG_BUILD_DIR) $(DL_DIR)/$(PKG_SOURCE)
	mv $(PKG_BUILD_DIR)/foo2zjs-master/* $(PKG_BUILD_DIR)/
	rmdir $(PKG_BUILD_DIR)/foo2zjs-master
	# --- 应用 patches 目录下的所有补丁文件 ---
	$(call PatchDir,$(PKG_BUILD_DIR),$(PATCH_DIR))
endef

# define Build/Compile
	# $(call Build/Compile/Default)
# endef

define Package/foo2zjs-extra/install
	$(INSTALL_DIR) $(1)/usr/share/foo2zjs
	$(MAKE) -C $(PKG_BUILD_DIR) DESTDIR=$(1) install-extra
endef

$(eval $(call BuildPackage,foo2zjs-extra))
