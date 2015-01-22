#
# Copyright (C) 2014 Mikeqin <Fengling.Qin@gmail.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mm-tools
PKG_VERSION:=git-$(shell git ls-remote https://github.com/Canaan-Creative/Avalon-extras master | cut -f1 | cut -c1-7)
PKG_REV:=master
PKG_RELEASE:=1
PKG_INSTALL:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_REV).tar.gz
PKG_SOURCE_URL:=https://github.com/Canaan-Creative/Avalon-extras.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=$(PKG_REV)

include $(INCLUDE_DIR)/package.mk

MAKE_PATH:=$(PKG_NAME)

define Package/mm-tools/Default
	MAINTAINER:="Mikeqin" <Fengling.Qin@gmail.com>
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=mm-tools
	URL:=https://github.com/Creative-Canaan/Avalon-extras.git
	DEPENDS:=
endef

define Package/mm-tools/description
mm-tools is a tool to reflash MM firmware for Avalon4, Support Raspberry Pi B only.
endef

define Package/mm-tools
	$(call Package/mm-tools/Default)
	TITLE+=(for Avalon4)
endef

define Build/Install
	@echo "Install nothing, Ignore install error"
endef

define Package/mm-tools/install
	$(INSTALL_DIR) $(1)/usr/bin
	cp $(PKG_BUILD_DIR)/$(MAKE_PATH)/$(PKG_NAME) $(1)/usr/bin
endef

$(eval $(call BuildPackage,mm-tools))
