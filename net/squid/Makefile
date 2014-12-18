#
# Copyright (C) 2006-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=squid
PKG_VERSION:=3.4.9
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=http://www.squid-cache.org/Versions/v3/3.4/
PKG_MD5SUM:=bb8ecbee8fa9fa8659b4349a78696fe7

PKG_BUILD_PARALLEL:=1
PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/squid/Default
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Web Servers/Proxies
  URL:=http://www.squid-cache.org/
endef

define Package/squid
  $(call Package/squid/Default)
  MENU:=1
  DEPENDS:=+libopenssl +libpthread +libnettle +librt +libnetfilter-conntrack +libstdcpp +libbsd +libltdl
  TITLE:=full-featured Web proxy cache
endef

define Package/squid/description
	Squid is a high-performance proxy caching server for web clients,
	supporting FTP, gopher, and HTTP data objects. Unlike traditional
	caching software, Squid handles all requests in a single,
	non-blocking, I/O-driven process.
endef

define Package/squid/conffiles
/etc/squid/mime.conf
/etc/squid/squid.conf
/etc/squid/errorpage.css
endef

define Package/squid-purge
  $(call Package/squid/Default)
  DEPENDS:=squid
  TITLE:=squid purge
endef

define Package/squid-client
  $(call Package/squid/Default)
  DEPENDS:=squid
  TITLE:=squid client
endef

define Package/squid-mod-cachemgr
  $(call Package/squid/Default)
  DEPENDS:=squid
  TITLE:=Web based proxy manager and reporting tool
endef

define Package/squid-mod-cachemgr/conffiles
/etc/squid/cachemgr.conf
endef

define Package/squid-mod-basic-auth-getpwnam
  $(call Package/squid/Default)
  DEPENDS:=squid
  TITLE:=getpwnam basic authentication helper
endef

define Package/squid-mod-basic-auth-ncsa
  $(call Package/squid/Default)
  DEPENDS:=squid
  TITLE:=NCSA basic authentication helper
endef

define Package/squid-mod-basic-auth-smb
  $(call Package/squid/Default)
  DEPENDS:=squid
  TITLE:=Samba basic authentication helper
endef

define Package/squid-mod-digest-auth-file
  $(call Package/squid/Default)
  DEPENDS:=squid
  TITLE:=Password file digest authentication helper
endef

define Package/squid-mod-external-acl-file-userip
  $(call Package/squid/Default)
  DEPENDS:=squid
  TITLE:=IP user external ACL helper
endef

define Package/squid-mod-external-acl-unix-group
  $(call Package/squid/Default)
  DEPENDS:=squid
  TITLE:=Unix group external ACL helper
endef

define Package/squid-mod-ntlm-auth-fake
  $(call Package/squid/Default)
  DEPENDS:=squid
  TITLE:=Fake NTLM authentication helper
endef

define Package/squid-mod-ntlm-auth-smb-lm
  $(call Package/squid/Default)
  DEPENDS:=squid
  TITLE:=Samba NTLM authentication helper
endef

CONFIGURE_ARGS += \
	HOSTCXX=g++ \
	--datadir=/usr/share/squid \
	--libexecdir=/usr/lib/squid \
	--sysconfdir=/etc/squid \
	--enable-shared \
	--enable-static \
	--enable-x-accelerator-vary \
	--with-pthreads \
	--with-dl \
	--enable-icmp \
	--enable-kill-parent-hack \
	--enable-arp-acl \
	--enable-ssl \
	--enable-htcp \
	--disable-snmp \
	--enable-err-languages=English \
	--enable-default-err-language=English \
	--enable-linux-netfilter \
	--enable-icmp \
	--enable-underscores \
	--enable-cache-digests \
	--enable-referer-log \
	--enable-delay-pools \
	--enable-useragent-log \
	--with-openssl=$(STAGING_DIR)/usr \
	--enable-auth \
	--enable-auth-basic="getpwnam NCSA SMB" \
	--enable-auth-ntlm="fake smb_lm" \
	--enable-auth-digest="file" \
	--enable-external-acl-helpers="file_userip unix_group" \
	--enable-storeio=ufs \
	--enable-epoll \
	--with-maxfd=4096 \
	--without-libcap \
	--with-krb5-config=no \
	--enable-ssl-crtd \
	--enable-icap-client

CONFIGURE_VARS += \
	ac_cv_header_linux_netfilter_ipv4_h=yes \
	ac_cv_epoll_works=yes \

define Build/Compile
	# pass INCLUDES to compile host sources against our OpenSSL, not the host one
	$(MAKE) -C $(PKG_BUILD_DIR)/lib \
		all
	$(MAKE) -C $(PKG_BUILD_DIR) \
		DESTDIR="$(PKG_INSTALL_DIR)" \
		install
endef

define BuildPlugin
  define Package/$(1)/install
	$(INSTALL_DIR) $$(1)/usr/lib/squid
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/squid/$(2) $$(1)/usr/lib/squid/
  endef

  $$(eval $$(call BuildPackage,$(1)))
endef

define Package/squid/install
	$(INSTALL_DIR) $(1)/etc/squid
	$(CP) $(PKG_INSTALL_DIR)/etc/squid/{squid,mime,errorpage}* $(1)/etc/squid/

	$(INSTALL_DIR) $(1)/usr/share/squid
	$(CP) $(PKG_INSTALL_DIR)/usr/share/squid/* $(1)/usr/share/squid/
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/squid $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/usr/lib/squid
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/squid/{ssl_crtd,unlinkd,pinger,log_file_daemon} $(1)/usr/lib/squid/
endef

define Package/squid-client/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/squidclient $(1)/usr/bin/
endef

define Package/squid-purge/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/purge $(1)/usr/bin/
endef

define Package/squid-mod-cachemgr/install
	$(INSTALL_DIR) $(1)/www/cgi-bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/squid/cachemgr.cgi $(1)/www/cgi-bin/
	$(INSTALL_DIR) $(1)/etc/squid
	$(CP) $(PKG_INSTALL_DIR)/etc/squid/cachemgr.conf $(1)/etc/squid/
endef

$(eval $(call RequireHeader,/usr/include/openssl/ssl.h, \
	$(PKG_NAME) requires the openssl development (named like libssl-dev, \
	depending of your package manager) package be installed on the host-system. \
))

$(eval $(call BuildPackage,squid))
$(eval $(call BuildPackage,squid-client))
$(eval $(call BuildPackage,squid-purge))
$(eval $(call BuildPackage,squid-mod-cachemgr))
$(eval $(call BuildPlugin,squid-mod-basic-auth-getpwnam,basic_getpwnam_auth))
$(eval $(call BuildPlugin,squid-mod-basic-auth-ncsa,basic_ncsa_auth))
$(eval $(call BuildPlugin,squid-mod-basic-auth-smb,basic_smb_auth))
$(eval $(call BuildPlugin,squid-mod-digest-auth-file,digest_file_auth))
$(eval $(call BuildPlugin,squid-mod-external-acl-file-userip,ext_file_userip_acl))
$(eval $(call BuildPlugin,squid-mod-external-acl-unix-group,ext_unix_group_acl))
$(eval $(call BuildPlugin,squid-mod-ntlm-auth-fake,ntlm_fake_auth))
$(eval $(call BuildPlugin,squid-mod-ntlm-auth-smb-lm,ntlm_smb_lm_auth))

