#
# Copyright (C) 2014-2016 Mikeqin <Fengling.Qin@gmail.com>
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

PKG_FIXUP:=autoreconf
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)/$(PKG_NAME)
PKG_UNPACK_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
PKG_UNPACK := $(SH_FUNC) $(call UNPACK_CMD,$(PKG_UNPACK_DIR)) $(call CRLF_CMD,$(PKG_UNPACK_DIR))

define Package/mm-tools/Default
	MAINTAINER:="Mikeqin" <Fengling.Qin@gmail.com>
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=mm-tools
	URL:=https://github.com/Creative-Canaan/Avalon-extras.git
	DEPENDS:=+libpthread +udev
endef

define Package/mm-tools/description
mm-tools is a tool to reflash MM firmware for Avalon4, 5, 6, 7.
It supports AUC and IIC interface.
endef

define Package/mm-tools/config
	menu "Configuration"
	source "$(SOURCE)/Config.in"
	endmenu
endef

define Package/mm-tools
	$(call Package/mm-tools/Default)
	TITLE+=(for Avalon4, 5, 6, 7)
endef

ifeq ($(CONFIG_MM_TOOLS_SOFT_CRC),y)
	CONFIGURE_ARGS += --enable-soft-crc
endif

define Build/Install
	@echo "Install nothing, Ignore install error"
endef

define Package/mm-tools/install
	$(INSTALL_DIR) $(1)/usr/bin
	cp $(PKG_BUILD_DIR)/$(PKG_NAME) $(1)/usr/bin
endef

$(eval $(call BuildPackage,mm-tools))
