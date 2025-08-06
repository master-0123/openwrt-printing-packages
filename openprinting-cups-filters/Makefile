## This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=openprinting-cups-filters
PKG_REALNAME:=cups-filters
PKG_VERSION:=2.0.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_REALNAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/OpenPrinting/cups-filters/releases/download/$(PKG_VERSION)/
PKG_MD5SUM:=ed7ef02215aa2845315800f6e790e840
PKG_BUILD_DIR:=$(BUILD_DIR)/cups-filters-$(PKG_VERSION)

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

EXTRA_CFLAGS+=-DHAVE_CPP_POPPLER_VERSION_H

define Package/openprinting-cups-filters
  PROVIDES:=foomatic-rip
  SECTION:=Net
  CATEGORY:=Network
  TITLE:=OpenPrinting CUPS filters
  DEPENDS:=+cups +libcupsfilters +libppd
  URL:=https://www.openprinting.org
  SUBMENU:=Printing
endef

define Package/openprinting-cups-filters/description
	CUPS filters maintained by OpenPrinting.
	The CUPS Filters package contains backends, filters and other software that was once part of the core CUPS distribution but is no longer maintained by Apple Inc.
endef

define Build/Configure
	$(call Build/Configure/Default, \
	--enable-imagefilters \
	--with-pdftops=gs \
	--with-gs-path=/usr/bin/gs \
	--with-pdftops-path=/usr/bin/gs \
	--disable-gnutls \
	--disable-openssl \
	--disable-cdsassl \
	--disable-ssl \
	--disable-gssapi \
	--disable-avahi \
	)
endef

define Build/Compile
	$(call Build/Compile/Default)
endef

define Package/openprinting-cups-filters/install
	$(INSTALL_DIR) $(1)/usr/bin $(1)/usr/lib/ $(1)/usr/share/
	$(CP) -r --preserve=links $(PKG_INSTALL_DIR)/usr/lib/cups $(1)/usr/lib/
	$(CP) --preserve=links $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin/
	$(CP) -r --preserve=links $(PKG_INSTALL_DIR)/usr/share/cups $(1)/usr/share/
	# 压缩 PPD 文件
	find $(PKG_INSTALL_DIR)/usr/share/ppd/cupsfilters -name "*.ppd" -exec gzip -9 -f {} \;
	$(INSTALL_DIR) $(1)/usr/share/cups/model
	$(CP) $(PKG_INSTALL_DIR)/usr/share/ppd/cupsfilters/*.ppd.gz $(1)/usr/share/cups/model/
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/lib $(1)/usr/share/ppdc
	$(CP) -r --preserve=links $(PKG_INSTALL_DIR)/usr/lib/cups $(1)/usr/lib/
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/share/ppdc/*.h $(1)/usr/share/ppdc/
	$(CP) -r --preserve=links $(PKG_INSTALL_DIR)/usr/share/cups $(1)/usr/share/
endef

define Package/preinst
#!/bin/sh
# Be on the safe side: get rid of any files from CUPS 1.5.X filters.
# See OpenPrinting's cups-filters-1.0.X/INSTALL
rm /usr/lib/cups/backend/serial
rm /usr/lib/cups/backend/parallel
rm /usr/lib/cups/filter/bannertops
rm /usr/lib/cups/filter/commandtoescpx
rm /usr/lib/cups/filter/commandtopclx
rm /usr/lib/cups/filter/imagetops
rm /usr/lib/cups/filter/imagetoraster
rm /usr/lib/cups/filter/pdftops
rm /usr/lib/cups/filter/rastertoescpx
rm /usr/lib/cups/filter/rastertopclx
rm /usr/lib/cups/filter/texttops
endef

define Package/postinst
#!/bin/sh
/etc/init.d/cupsd stop
/etc/init.d/cupsd start
endef

$(eval $(call BuildPackage,openprinting-cups-filters))
