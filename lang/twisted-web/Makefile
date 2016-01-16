#
# Copyright (C) 2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=twisted-web
PKG_Name:=Web
PKG_VERSION_MIN:=15.2
PKG_VERSION_FIX:=1
PKG_VERSION:=$(PKG_VERSION_MIN).$(PKG_VERSION_FIX)
PKG_RELEASE:=1

PKG_SOURCE:=Twisted$(PKG_Name)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=http://twistedmatrix.com/Releases/$(PKG_Name)/$(PKG_VERSION_MIN)/
PKG_MD5SUM:=178cba5e30f3b73a9c64b8fab0be577d

PKG_BUILD_DIR:=$(BUILD_DIR)/Twisted$(PKG_Name)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
$(call include_mk, python-package.mk)

define Package/twisted-web
  SUBMENU:=Python
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=Interfaces for Python
  URL:=https://twistedmatrix.com/
  DEPENDS:=+twisted-core
endef

define Package/twisted-web/description
  Twisted is an event-driven networking engine written in Python and licensed under the open source
endef

define Build/Compile
	$(call Build/Compile/PyMod,,\
		install --root="$(PKG_INSTALL_DIR)" --prefix="/usr" \
	)
endef

define PyPackage/twisted-web/filespec
+|/usr/lib/python$(PYTHON_VERSION)
endef

define Package/twisted-web/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin/
endef

$(eval $(call PyPackage,twisted-web))
$(eval $(call BuildPackage,twisted-web))
