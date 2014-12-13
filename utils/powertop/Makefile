#
# Copyright (C) 2006-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=powertop
PKG_VERSION:=2.7
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://01.org/sites/default/files/downloads/powertop/
PKG_MD5SUM:=e0d686e47daaf7e9d89031f7763432ef

PKG_INSTALL:=1
PKG_FIXUP:=autoreconf
PKG_BUILD_PARALLEL:=1
CONFIGURE_ARGS+=--disable-nls

include $(INCLUDE_DIR)/uclibc++.mk
include $(INCLUDE_DIR)/package.mk

define Package/powertop
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=PowerTOP
  DEPENDS:=+libncurses +libnl $(CXX_DEPENDS)
  URL:=http://www.lesswatts.org
endef

define Package/powertop/description
 PowerTOP is a Linux tool that helps you find those programs that are
 misbehaving while your computer is idle.
endef

define Package/powertop/install
	$(CP) $(PKG_INSTALL_DIR)/* $(1)
endef

$(eval $(call BuildPackage,powertop))
