#
# Copyright (C) 2012 Xiangfu Liu <xiangfu@openmobilefree.net>
#                            bitcoin: 12h6gdGnThW385JaX1LRMA8cXKmbYRTP8Q
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=cgminer
PKG_VERSION:=20121225
PKG_REV:=b9c7f3d169942417e04f13fab6e86d944aff37cb
# this is upstream version 2.10.2
PKG_RELEASE:=1
PKG_INSTALL:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_REV).tar.gz
PKG_SOURCE_URL:=git://github.com/ckolivas/cgminer.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=$(PKG_REV)

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/cgminer
	MAINTAINER:="Xiangfu Liu" <xiangfu@sharism.cc>
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=cgminer (FPGA Miner)
	URL:=https://github.com/ckolivas/cgminer
	DEPENDS:=+libcurl +libpthread +jansson +udev
endef

define Package/cgminer/description
Cgminer is a multi-threaded multi-pool GPU, FPGA and CPU miner with ATI GPU
monitoring, (over)clocking and fanspeed support for bitcoin and derivative
coins. Do not use on multiple block chains at the same time!
endef

CONFIGURE_ARGS += --disable-opencl --disable-adl --enable-icarus --enable-bitforce --without-curses
TARGET_LDFLAGS += -Wl,-rpath-link=$(STAGING_DIR)/usr/lib

define Build/Compile
	$(call Build/Compile/Default)
	( cd $(PKG_BUILD_DIR) && $(TARGET_CC) api-example.c -I compat/jansson -o cgminer-api; )
endef


define Package/cgminer/install
	$(INSTALL_DIR) $(1)/usr/bin $(1)/etc/init.d $(1)/etc/hotplug.d/usb

	$(INSTALL_BIN) $(PKG_BUILD_DIR)/cgminer-api $(1)/usr/bin

	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/cgminer $(1)/usr/bin
	$(INSTALL_BIN) $(FILES_DIR)/cgminer-monitor       $(1)/usr/bin
	$(INSTALL_BIN) $(FILES_DIR)/cgminer.init          $(1)/etc/init.d/cgminer

	$(CP)          $(FILES_DIR)/20-cgminer.hotplug $(1)/etc/hotplug.d/usb/20-cgminer
endef

$(eval $(call BuildPackage,cgminer))
