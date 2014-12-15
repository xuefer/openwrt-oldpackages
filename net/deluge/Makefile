#
# Copyright (C) 2008-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=deluge
PKG_VERSION:=1.3.11
PKG_RELEASE:=3

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://download.deluge-torrent.org/source/
PKG_MD5SUM:=5e36ba0a4bc3714e7056efda19d20772

include $(INCLUDE_DIR)/package.mk
$(call include_mk, python-package.mk)

define Package/deluge/Default
  SUBMENU:=BitTorrent
  SECTION:=net
  CATEGORY:=Network
  TITLE:=A lightweight BitTorrent client
  URL:=http://deluge-torrent.org/
endef

define Package/deluge
$(call Package/deluge/Default)
  TITLE+= (console UI & daemon)
  DEPENDS+=+python +rblibtorrent +python2-chardet +pyxdg +twisted-core +twisted-web +pyopenssl +python-setuptools
endef

define Package/deluge-ui-gtk
$(call Package/deluge/Default)
  TITLE+= (GTK+ UI)
  DEPENDS+=deluge +python-gtk
endef

define Package/deluge-ui-web
$(call Package/deluge/Default)
  TITLE+= (Web UI)
  DEPENDS+=deluge +mako
endef

define Package/deluge/description
  BitTorrent client with a client/server model.
endef

define Package/deluge/conffiles
/etc/config/deluge
endef

define Build/Compile
	$(call Build/Compile/PyMod,,\
		install --prefix="$(PKG_INSTALL_DIR)/usr" \
		--old-and-unmanageable \
	)

	$(SED) 's,#!.*/host/bin/python.*,#!/usr/bin/$(PYTHON),' $(PKG_INSTALL_DIR)/usr/bin/*
endef

define PyPackage/deluge/filespec
+|$(PYTHON_PKG_DIR)
-|$(PYTHON_PKG_DIR)/deluge/ui/gtkui
-|$(PYTHON_PKG_DIR)/deluge/ui/web
endef

define PyPackage/deluge/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) \
	    $(PKG_INSTALL_DIR)/usr/bin/* \
	    $(1)/usr/bin/
	rm -rf $(1)/usr/bin/deluge-gtk
	rm -rf $(1)/usr/bin/deluge-web

	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) ./files/deluge.config $(1)/etc/config/deluge

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/deluge.init $(1)/etc/init.d/deluge
	$(SED) 's#/usr/bin/python2.6#/usr/bin/$(PYTHON)#' $(1)/etc/init.d/deluge
endef

define PyPackage/deluge-ui-gtk/filespec
+|$(PYTHON_PKG_DIR)/deluge/ui/gtkui
endef

define PyPackage/deluge-ui-gtk/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) \
	    $(PKG_INSTALL_DIR)/usr/bin/deluge-gtk \
	    $(1)/usr/bin/
endef

define PyPackage/deluge-ui-web/filespec
+|$(PYTHON_PKG_DIR)/deluge/ui/web
endef

define PyPackage/deluge-ui-web/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) \
	    $(PKG_INSTALL_DIR)/usr/bin/deluge-web \
	    $(1)/usr/bin/
endef

$(eval $(call PyPackage,deluge))
$(eval $(call BuildPackage,deluge))
$(eval $(call PyPackage,deluge-ui-gtk))
$(eval $(call BuildPackage,deluge-ui-gtk))
$(eval $(call PyPackage,deluge-ui-web))
$(eval $(call BuildPackage,deluge-ui-web))
