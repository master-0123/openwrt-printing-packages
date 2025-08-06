#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/nls.mk

PKG_NAME:=libcupsfilters
PKG_VERSION:=2.1.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=https://github.com/OpenPrinting/libcupsfilters/releases/download/$(PKG_VERSION)/
PKG_HASH:=6c303e36cfde05a6c88fb940c62b6a18e7cdbfb91f077733ebc98f104925ce36

PKG_LICENSE:=LGPL-2.1-or-later
PKG_LICENSE_FILES:=COPYING
PKG_CPE_ID:=cpe:/a:openprinting:libcupsfilters
 
include $(INCLUDE_DIR)/package.mk

define Package/libcupsfilters
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=OpenPrinting CUPS Filters library
  URL:=https://github.com/OpenPrinting/libcupsfilters
  DEPENDS:=+cups +fontconfig +libtiff +libjpeg +libpng +glib2 +libdbus +libexif +qpdf +poppler +lcms2
  SUBMENU:=Printing
endef

define Package/libcupsfilters/description
  libcupsfilters is the main filter library from the OpenPrinting CUPS Filters project,
  providing common functions for CUPS filters and backends.
endef

define Build/Configure
	$(call Build/Configure/Default, \
	--disable-static \
	--enable-poppler \
	--enable-dbus \
	--disable-mutool \
	--with-gs-path=/usr/bin/gs \
	--enable-imagefilters \
	CFLAGS="$$(TARGET_CFLAGS) -I$(STAGING_DIR)/usr/include" \
	CPPFLAGS="$$(TARGET_CPPFLAGS) -I$(STAGING_DIR)/usr/include" \
	LDFLAGS="$$(TARGET_LDFLAGS)" \
	)
endef

define Build/Compile
	$(call Build/Compile/Default)
	$(MAKE) -C $(PKG_BUILD_DIR) DESTDIR=$(PKG_INSTALL_DIR) install
endef

define Package/libcupsfilters/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) --preserve=links $(PKG_INSTALL_DIR)/usr/lib/libcupsfilters.* $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/share/cups/banners $(1)/usr/share/cups/charsets $(1)/usr/share/cups/data
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/share/cups/banners/* $(1)/usr/share/cups/banners/
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/share/cups/charsets/* $(1)/usr/share/cups/charsets/
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/share/cups/data/* $(1)/usr/share/cups/data/
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) --preserve=links $(PKG_INSTALL_DIR)/usr/lib/libcupsfilters.* $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/* $(1)/usr/lib/pkgconfig/
	$(INSTALL_DIR) $(1)/usr/include/cupsfilters
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/include/cupsfilters/* $(1)/usr/include/cupsfilters/
endef

$(eval $(call BuildPackage,libcupsfilters))
