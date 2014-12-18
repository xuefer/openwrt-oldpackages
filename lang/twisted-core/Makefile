#
# Copyright (C) 2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=twisted-core
PKG_Name:=Core
PKG_VERSION_MIN:=14.0
PKG_VERSION_FIX:=2
PKG_VERSION:=$(PKG_VERSION_MIN).$(PKG_VERSION_FIX)
PKG_RELEASE:=1

PKG_SOURCE:=Twisted$(PKG_Name)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=http://twistedmatrix.com/Releases/$(PKG_Name)/$(PKG_VERSION_MIN)/
PKG_MD5SUM:=399b034eab5bce742e6cc03c0c4709eb

PKG_BUILD_DIR:=$(BUILD_DIR)/Twisted$(PKG_Name)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
$(call include_mk, python-package.mk)

define Package/twisted-core
  SUBMENU:=Python
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=Interfaces for Python
  URL:=https://twistedmatrix.com/
  DEPENDS:=+zope-interface
endef

define Package/twisted-core/description
  Twisted is an event-driven networking engine written in Python and licensed under the open source
endef

define Build/Compile
	$(call Build/Compile/PyMod,,\
		install --prefix="$(PKG_INSTALL_DIR)/usr" \
	)
endef

define PyPackage/twisted-core/filespec
+|/usr/lib/python$(PYTHON_VERSION)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)$(PYTHON_PKG_DIR)
	$(CP) \
		$(PKG_INSTALL_DIR)$(PYTHON_PKG_DIR)/* \
		$(1)$(PYTHON_PKG_DIR)
endef

define Package/twisted-core/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin/
endef

$(eval $(call PyPackage,twisted-core))
$(eval $(call BuildPackage,twisted-core))
