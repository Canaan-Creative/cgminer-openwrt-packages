#
# Author: Jimmy Situ <web@jimmystone.cn>
# Address:1KHujLT4AzQwQKSLEUSbcergqv7fMnQNXA 
#
# This is free and unencumbered software released into the public domain.
# For details see the UNLICENSE file at the root of the source tree.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=bitcoind

ifeq ($(CONFIG_BITCOIND),y)
	PKG_VERSION:=v0.10.0
	PKG_REV:=080457c4ee97e38aa8e59de89bf3d78d1de142aa
endif

PKG_RELEASE:=1
PKG_INSTALL:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_REV).tar.bz2
ifeq ($(CONFIG_BITCOIND),y)
	PKG_SOURCE_URL:=git://github.com/bitcoin/bitcoin.git
endif

PKG_SOURCE_PROTO:=git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=$(PKG_REV)

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=Bitcoin full node
	URL:=https://github.com/bitcoin/bitcoin
	DEPENDS := +libcurl +libpthread +jansson +udev +libncurses 
	DEPENDS += +boost-chrono +boost-filesystem +boost-program_options +boost-thread +boost-test
	DEPENDS += +libopenssl +libstdcpp
endef

define Package/$(PKG_NAME)/description
Bitcoind is a bitcoin full node
endef

define Package/$(PKG_NAME)/config
	menu "Configuration"
	depends on PACKAGE_bitcoind
	source "$(SOURCE)/Config.in"
	endmenu
endef

TARGET_CFLAGS  += -std=c99
TARGET_LDFLAGS += -Wl,-rpath-link=$(STAGING_DIR)/usr/lib

ifeq ($(CONFIG_BITCOIND),y)
	CONFIGURE_ARGS += --without-miniupnpc
	CONFIGURE_ARGS += --disable-wallet
	CONFIGURE_ARGS += --with-boost-libdir=$(STAGING_DIR)/usr/lib
endif

define Build/Compile
	$(call Build/Compile/Default)
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_DIR) $(1)/etc/config

	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/bitcoind  	$(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/bitcoin-cli   $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/test_bitcoin  $(1)/usr/bin

ifeq ($(CONFIG_BITCOIND),y)
	$(INSTALL_BIN) $(FILES_DIR)/bitcoind-monitor        $(1)/usr/bin/bitcoind-monitor
	$(INSTALL_BIN) $(FILES_DIR)/bitcoind.init           $(1)/etc/init.d/bitcoind
	$(CP)          $(FILES_DIR)/bitcoind.config         $(1)/etc/config/bitcoind
	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(CP)          $(FILES_DIR)/bitcoind.uci-defaults   $(1)/etc/uci-defaults/01-bitcoind
	$(INSTALL_DIR) $(1)/root/.bitcoin
	$(CP)          $(FILES_DIR)/bitcoin.conf            $(1)/root/.bitcoin/bitcoin.conf
endif

endef

$(eval $(call BuildPackage,$(PKG_NAME)))
