#
# Copyright (C) 2007-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=argus
PKG_VERSION:=v5.0.2
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/openargus/argus.git
PKG_SOURCE_DATE:=2024-06-20
PKG_SOURCE_VERSION:=b1312f51826a53912db1e88d3b9a879b841158b5

#PKG_SOURCE:=$(PKG_VERSION).tar.gz
#PKG_SOURCE_URL:=https://github.com/openargus/argus/archive/refs/tags/
#PKG_MD5SUM:=b21ae02943c4407cd56205fb9f5918db

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_BUILD_PARALLEL:=1
HOST_BUILD_DEPENDS:=libtirpc/host
PKG_BUILD_DEPENDS:=libtirpc/host

PKG_MAINTAINER:=Carter Bullard <carter@qosient.com>
PKG_LICENSE:=GPL-2.0

PKG_INSTALL:=1

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk

define Package/argus
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libtirpc +libpcap +libpthread +zlib
  TITLE:=Network Audit Record Generation and Utilization System 
  URL:=http://www.qosient.com/
endef

define Package/bridge/description
  Network Audit Record Generation and Utilization System
endef

TARGET_CFLAGS+= -I$(STAGING_DIR)/usr/include/tirpc

define Build/Configure
  $(call Build/Configure/Default)
endef

define Package/argus/conffiles
	/etc/argus.conf
endef

define Package/argus/install
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/argus.init $(1)/etc/init.d/argus
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) ./files/argus.conf $(1)/etc/config/argus.conf
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/argus $(1)/usr/sbin/
endef

$(eval $(call BuildPackage,argus))
