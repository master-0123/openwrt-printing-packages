include $(TOPDIR)/rules.mk

PKG_NAME:=libppd
PKG_VERSION:=2.1.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=https://github.com/OpenPrinting/libppd/releases/download/$(PKG_VERSION)/
PKG_HASH:=3fa341cc03964046d2bf6b161d80c1b4b2e20609f38d860bcaa11cb70c1285e4

PKG_LICENSE:=LGPL-2.1-or-later
PKG_LICENSE_FILES:=COPYING
PKG_CPE_ID:=cpe:/a:openprinting:libppd

PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/libppd
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=OpenPrinting PPD file handling library
  URL:=https://github.com/OpenPrinting/libppd
  DEPENDS:=+libcupsfilters +cups +ghostscript
  SUBMENU:=Printing
endef

define Package/libppd/description
  libppd is a library for handling PostScript Printer Description (PPD) files,
  part of the OpenPrinting CUPS Filters project.
endef

CONFIGURE_ARGS += \
	--disable-static \
	--with-pdftops=gs \
	--with-gs-path=/usr/bin/gs \
	--with-pdftops-path=/usr/bin/gs
#	--with-cups-config=$(STAGING_DIR)/usr/bin/cups-config \

define Build/Compile
	$(call Build/Compile/Default)
	$(MAKE) -C $(PKG_BUILD_DIR) DESTDIR=$(PKG_INSTALL_DIR) install
endef

define Package/libppd/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) --preserve=links $(PKG_INSTALL_DIR)/usr/lib/libppd.* $(1)/usr/lib/
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/ppd
	$(CP) $(PKG_INSTALL_DIR)/usr/include/ppd/*.h $(1)/usr/include/ppd/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) --preserve=links $(PKG_INSTALL_DIR)/usr/lib/libppd.* $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/libppd.pc $(1)/usr/lib/pkgconfig/
endef

$(eval $(call BuildPackage,libppd))