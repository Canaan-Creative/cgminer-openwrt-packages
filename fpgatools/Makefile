#
# Copyright (C) 2012 Xiangfu Liu <xiangfu@openmobilefree.net>
#                            bitcoin: 12h6gdGnThW385JaX1LRMA8cXKmbYRTP8Q
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=fpgatools
PKG_VERSION:=$(shell date +%Y%m%d)
PKG_REV:=HEAD
PKG_RELEASE:=1
PKG_INSTALL:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_REV).tar.gz
PKG_SOURCE_URL:=git://github.com/Wolfgang-Spraul/fpgatools.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=$(PKG_REV)

include $(INCLUDE_DIR)/package.mk

define Package/fpgatools/Default
	MAINTAINER:="Xiangfu Liu" <xiangfu@sharism.cc>
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=fpgatools
	URL:=https://github.com/ckolivas/fpgatools
	DEPENDS:=+libusb-compat +libftdi
endef

define Package/fpgatools/description
fpgatools is a toolchain to program field-programmable gate arrays (FPGAs)
endef

TARGET_LDFLAGS += -lusb -lftdi
define Build/Compile
	$(call Build/Compile/Default, fp2bit, bit2fp)
	$(MAKE_VARS) $(MAKE) -C $(PKG_BUILD_DIR)/mini-jtag \
		$(MAKE_FLAGS) \
		DESTDIR="$(PKG_INSTALL_DIR)" \
		all install
endef

define Package/fpgatools
	$(call Package/fpgatools/Default)
	TITLE+=(fpgatools)
endef

define Package/fpgatools/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_DIR) $(1)/usr/lib

	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/local/bin/fp2bit $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/local/bin/bit2fp $(1)/usr/bin
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/local/lib/libfpga-* \
		$(1)/usr/lib/
endef

define Package/mini-jtag
	$(call Package/fpgatools/Default)
	DEPENDS:=+libusb-compat +libftdi
	TITLE+=(mini-jtag)
endef

define Package/mini-jtag/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/local/bin/mini-jtag $(1)/usr/bin
endef

$(eval $(call BuildPackage,fpgatools))
$(eval $(call BuildPackage,mini-jtag))
