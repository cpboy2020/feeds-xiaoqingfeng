include $(TOPDIR)/rules.mk

PKG_NAME:=chinadns-ng
PKG_VERSION:=2020.4.10
PKG_RELEASE:=4-xiaoqingfengMod

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/zfl9/chinadns-ng.git
PKG_MIRROR_HASH:=d6450e0731602fa24d437912a4dd4b6d74000237e8ccf334a175c96285accb86
PKG_SOURCE_VERSION:=90e9f263fa6b4954d52dfa2f36948968269bc73b

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION)
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)/$(PKG_SOURCE_SUBDIR)

PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0

PKG_LICENSE:=GPL-3.0
PKG_LICENSE_FILES:=LICENSE
PKG_MAINTAINER:=pexcn <i@pexcn.me>

include $(INCLUDE_DIR)/package.mk

define Package/chinadns-ng
	SECTION:=net
	CATEGORY:=Network
	TITLE:=ChinaDNS next generation, refactoring with epoll and ipset
	URL:=https://github.com/zfl9/chinadns-ng
	DEPENDS:=+ipset
endef

define Package/chinadns-ng/description
ChinaDNS next generation, refactoring with epoll and ipset.
endef

define Package/chinadns-ng/conffiles
/etc/config/chinadns-ng
/etc/chinadns-ng/chnroute.txt
/etc/chinadns-ng/chnroute6.txt
/etc/chinadns-ng/gfwlist.txt
/etc/chinadns-ng/chinalist.txt
endef

define Package/chinadns-ng/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/chinadns-ng $(1)/usr/bin
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) files/chinadns-ng.init $(1)/etc/init.d/chinadns-ng
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) files/chinadns-ng.config $(1)/etc/config/chinadns-ng
	$(INSTALL_DIR) $(1)/etc/chinadns-ng
	$(INSTALL_DATA) files/chnroute.txt $(1)/etc/chinadns-ng
	$(INSTALL_DATA) files/chnroute6.txt $(1)/etc/chinadns-ng
	$(INSTALL_DATA) files/gfwlist.txt $(1)/etc/chinadns-ng
	$(INSTALL_DATA) files/chinalist.txt $(1)/etc/chinadns-ng
	$(INSTALL_BIN) files/updateChinadns-ngConfig.sh $(1)/etc/chinadns-ng
	$(INSTALL_BIN) files/update-chnlist.sh $(1)/etc/chinadns-ng
	$(INSTALL_BIN) files/update-chnroute.sh $(1)/etc/chinadns-ng
	$(INSTALL_BIN) files/update-chnroute6.sh $(1)/etc/chinadns-ng
	$(INSTALL_BIN) files/update-gfwlist.sh $(1)/etc/chinadns-ng
endef

define Package/chinadns-ng/postrm
#!/bin/sh
rmdir --ignore-fail-on-non-empty /etc/chinadns-ng
exit 0
endef

$(eval $(call BuildPackage,chinadns-ng))
