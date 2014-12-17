#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mm-tools
PKG_VERSION:=$(shell date +%Y%m%d)
PKG_REV:=HEAD
PKG_RELEASE:=1
PKG_INSTALL:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_REV).tar.gz
PKG_SOURCE_URL:=git://github.com/Creative-Canaan/Avalon-extras.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=$(PKG_REV)

include $(INCLUDE_DIR)/package.mk

define Package/mm-tools/Default
	MAINTAINER:="Xiangfu Liu" <xiangfu@sharism.cc>
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=mm-tools
	URL:=https://github.com/Creative-Canaan/Avalon-extras.git
	DEPENDS:=
endef

define Package/fpgatools/description
	mm-tools is a tool to reflash field-programmable gate arrays (FPGAs)
endef

define Package/mm-tools
	$(call Package/mm-tools/Default)
	TITLE+=(mm-tools)
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR)/mm-tools DESTDIR="$(PKG_INSTALL_DIR)"
endef

define Build/Clean
	$(MAKE) -C $(PKG_BUILD_DIR)/mm-tools clean
endef

define Build/Install
	$(INSTALL_DIR) $(1)/usr/bin
	cp $(PKG_BUILD_DIR)/mm-tools/mm-tools $(1)/usr/bin
endef

define Package/mm-tools/install
	$(INSTALL_DIR) $(1)/usr/bin
	cp $(PKG_BUILD_DIR)/mm-tools/mm-tools $(1)/usr/bin
endef

$(eval $(call BuildPackage,mm-tools))
