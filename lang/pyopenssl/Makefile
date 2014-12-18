#
# Copyright (C) 2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=pyopenssl
PKG_VERSION:=0.13
PKG_RELEASE:=1

PKG_SOURCE:=pyOpenSSL-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://pypi.python.org/packages/source/p/pyOpenSSL/
PKG_MD5SUM:=767bca18a71178ca353dff9e10941929

PKG_BUILD_DIR:=$(BUILD_DIR)/pyOpenSSL-$(PKG_VERSION)
PKG_BUILD_DEPENDS:=python

include $(INCLUDE_DIR)/package.mk
$(call include_mk, python-package.mk)

define Package/pyopenssl
  SUBMENU:=Python
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=pyopenssl
  URL:=http://pyopenssl.sourceforge.net/
  DEPENDS:=+python +libopenssl
endef

define Package/pyopenssl/description
  Python interface to the OpenSSL library.
endef

define PyPackage/pyopenssl/filespec
+|/usr/lib/python$(PYTHON_VERSION)
endef

define Build/Compile
	$(if $(Build/Compile/PyMod),,@echo Python packaging code not found.; false)
	$(call Build/Compile/PyMod,., \
		install --prefix="$(PKG_INSTALL_DIR)/usr", \
	)
endef

$(eval $(call PyPackage,pyopenssl))
$(eval $(call BuildPackage,pyopenssl))
