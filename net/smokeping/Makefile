#
# Copyright (C) 2006 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=smokeping
PKG_VERSION:=2.6.9
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://oss.oetiker.ch/smokeping/pub/
PKG_MD5SUM:=0c2361b734866dd37facf2af3f8f7144

include $(INCLUDE_DIR)/package.mk

define Package/smokeping
  SECTION:=net
  CATEGORY:=Network
  TITLE:=SmokePing keeps track of your network latency
  URL:=http://oss.oetiker.ch/smokeping/
  DEPENDS:=+perl +perlbase-cgi +perl-rrd +perlbase-digest
endef

define Package/smokeping/description
  SmokePing keeps track of your network latency:
  . Best of breed latency visualisation.
  . Interactive graph explorer.
  . Wide range of latency measurment plugins.
  . Master/Slave System for distributed measurement.
  . Highly configurable alerting system.
  . Live Latency Charts with the most 'interesting' graphs.
  . Free and OpenSource Software written in Perl written by Tobi Oetiker, the creator of MRTG and RRDtool
endef
  
#define Build/Configure
#        (cd $(PKG_BUILD_DIR); touch \
#		configure \
#		stamp-h.in \
#		config.h.in \
#	);
#	$(call Build/Configure/Default,)
#endef
#
#define Build/Compile
#	$(MAKE) CC="$(TARGET_CC)" CFLAGS="$(TARGET_CFLAGS)" -C $(PKG_BUILD_DIR) clean $(PKG_NAME)
#	mv $(PKG_BUILD_DIR)/$(PKG_NAME) $(PKG_BUILD_DIR)/$(PKG_NAME)4
#	$(MAKE) CC="$(TARGET_CC)" CFLAGS="$(TARGET_CFLAGS) -DIPV6=1" -C $(PKG_BUILD_DIR) clean $(PKG_NAME)
#	mv $(PKG_BUILD_DIR)/$(PKG_NAME) $(PKG_BUILD_DIR)/$(PKG_NAME)6
#endef

define Package/smokeping/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_BUILD_DIR)/smokeping $(1)/usr/bin/
	ln -sf smokeping $(1)/usr/bin/smokeping
endef

$(eval $(call BuildPackage,smokeping))
#
# Copyright (C) 2006 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=smokeping
PKG_VERSION:=2.6.9
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://oss.oetiker.ch/smokeping/pub/
PKG_MD5SUM:=0c2361b734866dd37facf2af3f8f7144

include $(INCLUDE_DIR)/package.mk

define Package/smokeping
  SECTION:=net
  CATEGORY:=Network
  TITLE:=SmokePing keeps track of your network latency
  URL:=http://oss.oetiker.ch/smokeping/
  DEPENDS:=+perl +perlbase-cgi +perl-rrd +perlbase-digest
endef

define Package/smokeping/description
  SmokePing keeps track of your network latency:
  . Best of breed latency visualisation.
  . Interactive graph explorer.
  . Wide range of latency measurment plugins.
  . Master/Slave System for distributed measurement.
  . Highly configurable alerting system.
  . Live Latency Charts with the most 'interesting' graphs.
  . Free and OpenSource Software written in Perl written by Tobi Oetiker, the creator of MRTG and RRDtool
endef
  
#define Build/Configure
#        (cd $(PKG_BUILD_DIR); touch \
#		configure \
#		stamp-h.in \
#		config.h.in \
#	);
#	$(call Build/Configure/Default,)
#endef
#
#define Build/Compile
#	$(MAKE) CC="$(TARGET_CC)" CFLAGS="$(TARGET_CFLAGS)" -C $(PKG_BUILD_DIR) clean $(PKG_NAME)
#	mv $(PKG_BUILD_DIR)/$(PKG_NAME) $(PKG_BUILD_DIR)/$(PKG_NAME)4
#	$(MAKE) CC="$(TARGET_CC)" CFLAGS="$(TARGET_CFLAGS) -DIPV6=1" -C $(PKG_BUILD_DIR) clean $(PKG_NAME)
#	mv $(PKG_BUILD_DIR)/$(PKG_NAME) $(PKG_BUILD_DIR)/$(PKG_NAME)6
#endef

define Package/smokeping/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_BUILD_DIR)/smokeping $(1)/usr/bin/
	ln -sf smokeping $(1)/usr/bin/smokeping
endef

$(eval $(call BuildPackage,smokeping))
