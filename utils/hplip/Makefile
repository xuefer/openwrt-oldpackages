#
# Copyright (C) 2006-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=hplip
PKG_VERSION:=3.16.11
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/hplip
PKG_HASH:=f6e20cacb4891e4e60fc5de2213a10f8d0c68840f9b511aa38cfca0cb29f9b24

PKG_CONFIG_DEPENDS:=CONFIG_PACKAGE_hplip-sane python
PKG_BUILD_DEPENDS:=python python/host
PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk
$(call include_mk, python-package.mk)

define Package/hplip/default
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=HP Linux Imaging and Printing
  URL:=http://sourceforge.net/projects/hplip/
endef

define Package/hplip
  $(call Package/hplip/default)
  DEPENDS+=+libjpeg +libtiff +libusb-compat +cups
endef

define Package/hplip/description
	HPLIP is an HP developed solution for printing, scanning, and faxing with HP inkjet and laser based printers in Linux.
endef

define Package/hplip-sane
  $(call Package/hplip/default)
  DEPENDS+=+hplip +PACKAGE_hilip-sane:sane-libs
endef

define Package/hplip-sane/description
	HPLIP is an HP developed solution for printing, scanning, and faxing with HP inkjet and laser based printers in Linux.
endef

define Package/hplip-filter
  $(call Package/hplip/default)
  DEPENDS+=+hplip +libcupsimage
endef

define Package/hplip-filter/description
	HPLIP is an HP developed solution for printing, scanning, and faxing with HP inkjet and laser based printers in Linux.
endef

CONFIGURE_ARGS += \
	--enable-libusb01_build \
	--disable-gui-build \
	--disable-network-build \
	--disable-fax-build \
	$(if $(CONFIG_PACKAGE_hiplp-sane),,--disable-scan-build) \
	--disable-pp-build \
	--disable-doc-build \
	--disable-foomatic-xml-install \
	--disable-dbus-build

define Build/Configure
	$(call Build/Configure/Default,\
		$(CONFIGURE_ARGS),\
		ac_cv_lib_cups_cupsDoFileRequest=yes \
		LIBS="-lz -ljpeg -lusb -lcups -lpng -ltiff" \
	)
endef

define Package/hplip/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/.libs/libhpip.so* $(1)/usr/lib/
	$(CP) $(PKG_BUILD_DIR)/.libs/libhpmud.so* $(1)/usr/lib/

	$(INSTALL_DIR) $(1)/usr/lib/cups/backend
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/.libs/hp $(1)/usr/lib/cups/backend

	$(INSTALL_DIR) $(1)/etc/hp
	$(CP) $(PKG_BUILD_DIR)/hplip.conf $(1)/etc/hp/hplip.conf

	$(INSTALL_DIR) $(1)/usr/share/hplip/data/models/
	$(CP) $(PKG_BUILD_DIR)/data/models/models.dat $(1)/usr/share/hplip/data/models/

	$(INSTALL_DIR) $(1)/etc/hotplug.d/usb/
	$(INSTALL_BIN) ./files/20-hplip $(1)/etc/hotplug.d/usb/
endef

define Package/hplip/conffiles
/etc/hp/hplip.conf
/etc/hotplug.d/usb/20-hplip
endef

define Package/hplip-sane/install
	$(INSTALL_DIR) $(1)/usr/lib/sane
	$(CP) $(PKG_BUILD_DIR)/.libs/libsane-hpaio.so* $(1)/usr/lib/sane

	$(INSTALL_DIR) $(1)/etc/sane.d/dll.d/
	$(INSTALL_DATA) ./files/hplib.conf $(1)/etc/sane.d/dll.d/hplib
endef

define Package/hplip-sane/conffiles
/etc/sane.d/dll.d/hplib
endef

define Package/hplip-filter/install
	$(INSTALL_DIR) $(1)/usr/lib/cups/filter
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/hpcups $(1)/usr/lib/cups/filter
endef

$(eval $(call BuildPackage,hplip))
$(eval $(call BuildPackage,hplip-sane))
$(eval $(call BuildPackage,hplip-filter))
