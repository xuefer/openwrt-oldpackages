include $(TOPDIR)/rules.mk

PKG_NAME:=hdrecover
PKG_VERSION:=0.5
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/$(PKG_NAME)
PKG_MD5SUM:=1cbe15f790fe383a20375b97aa3e5d04

include $(INCLUDE_DIR)/uclibc++.mk
include $(INCLUDE_DIR)/package.mk

TARGET_CXXFLAGS += "-fno-rtti"

define Package/hdrecover
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=disc
  DEPENDS:= $(CXX_DEPENDS)
  TITLE:=Attempts to recover a hard disk that has bad blocks on it.
  URL:=http://hdrecover.sourceforge.net/
endef

define Package/hdrecover/description
 get/set SATA/IDE device parameters
endef

define Package/hdrecover/install
	$(INSTALL_DIR) $(1)/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/$(PKG_NAME) $(1)/sbin
endef

$(eval $(call BuildPackage,hdrecover))
