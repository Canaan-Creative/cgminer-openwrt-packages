#
# Author: Xiangfu Liu <xiangfu@openmobilefree.net>
#         Mikeqin <Fengling.Qin@gmail.com>
# Address: 12h6gdGnThW385JaX1LRMA8cXKmbYRTP8Q
#
# This is free and unencumbered software released into the public domain.
# For details see the UNLICENSE file at the root of the source tree.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=cgminer

ifeq ($(CONFIG_CGMINER_AVALON4),y)
	PKG_VERSION:=git-$(shell git ls-remote https://github.com/Canaan-Creative/cgminer avalon4 | cut -f1 | cut -c1-7)
	PKG_REV:=avalon4
else
	PKG_VERSION:=4.6.0
	PKG_REV:=06b44fcc2ed64a3e0d8288287d28176132433642
endif
ifeq ($(CONFIG_CGMINER_AVALON6),y)
	PKG_VERSION:=git-$(shell git ls-remote https://github.com/Canaan-Creative/cgminer avalon4 | cut -f1 | cut -c1-7)
	PKG_REV:=avalon4
endif
ifeq ($(CONFIG_CGMINER_AVALON7),y)
	PKG_VERSION:=git-$(shell git ls-remote https://github.com/Canaan-Creative/cgminer master | cut -f1 | cut -c1-7)
	PKG_REV:=master
endif
ifeq ($(CONFIG_CGMINER_AVALON8),y)
	PKG_VERSION:=git-$(shell git ls-remote https://github.com/Canaan-Creative/cgminer avalon8 | cut -f1 | cut -c1-7)
	PKG_REV:=avalon8
ifeq ($(CONFIG_CGMINER_AVALON8_LP),y)
	PKG_VERSION:=git-$(shell git ls-remote https://github.com/Canaan-Creative/cgminer avalon8_lp | cut -f1 | cut -c1-7)
	PKG_REV:=avalon8_lp
endif
ifeq ($(CONFIG_CGMINER_AVALON9),y)
	PKG_VERSION:=git-$(shell git ls-remote https://github.com/Canaan-Creative/cgminer avalon9 | cut -f1 | cut -c1-7)
	PKG_REV:=avalon9
endif
ifeq ($(CONFIG_CGMINER_AVALON911),y)
	PKG_VERSION:=git-$(shell git ls-remote https://github.com/Canaan-Creative/cgminer avalon911 | cut -f1 | cut -c1-7)
	PKG_REV:=avalon911
endif
ifeq ($(CONFIG_CGMINER_AVALONLC3),y)
	PKG_VERSION:=git-$(shell git ls-remote https://github.com/Canaan-Creative/cgminer avalonlc3 | cut -f1 | cut -c1-7)
	PKG_REV:=avalonlc3
endif

PKG_RELEASE:=1
PKG_INSTALL:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_REV).tar.bz2
ifeq ($(CONFIG_CGMINER_AVALON4),y)
	PKG_SOURCE_URL:=git://github.com/Canaan-Creative/cgminer.git
else
	PKG_SOURCE_URL:=git://github.com/ckolivas/cgminer.git
endif
ifeq ($(CONFIG_CGMINER_AVALON6),y)
	PKG_SOURCE_URL:=git://github.com/Canaan-Creative/cgminer.git
endif
ifeq ($(CONFIG_CGMINER_AVALON7),y)
	PKG_SOURCE_URL:=git://github.com/Canaan-Creative/cgminer.git
endif
ifeq ($(CONFIG_CGMINER_AVALON8),y)
	PKG_SOURCE_URL:=git://github.com/Canaan-Creative/cgminer.git
endif
ifeq ($(CONFIG_CGMINER_AVALON8_LP),y)
	PKG_SOURCE_URL:=git://github.com/Canaan-Creative/cgminer.git
endif
ifeq ($(CONFIG_CGMINER_AVALON9),y)
	PKG_SOURCE_URL:=git://github.com/Canaan-Creative/cgminer.git
endif
ifeq ($(CONFIG_CGMINER_AVALON911),y)
	PKG_SOURCE_URL:=git://github.com/Canaan-Creative/cgminer.git
endif
ifeq ($(CONFIG_CGMINER_AVALONLC3),y)
	PKG_SOURCE_URL:=git://github.com/Canaan-Creative/cgminer.git
endif
PKG_SOURCE_PROTO:=git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=$(PKG_REV)

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/cgminer
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=cgminer
	URL:=https://github.com/ckolivas/cgminer
ifeq ($(CONFIG_TARGET_brcm2708_RaspberryPi),)
	DEPENDS:=+libcurl +libpthread +jansson +udev +libusb-1.0
else
	DEPENDS:=+libcurl +libpthread +jansson +udev +libusb-1.0 +libncurses
endif
endef

define Package/cgminer/description
Cgminer is a multi-threaded multi-pool GPU, FPGA and CPU miner with ATI GPU
monitoring, (over)clocking and fanspeed support for bitcoin and derivative
coins. Do not use on multiple block chains at the same time!
endef

define Package/cgminer/config
	menu "Configuration"
	depends on PACKAGE_cgminer
	source "$(SOURCE)/Config.in"
	endmenu
endef

TARGET_LDFLAGS += -Wl,-rpath-link=$(STAGING_DIR)/usr/lib

ifeq ($(CONFIG_CGMINER_AVALON1),y)
	CONFIGURE_ARGS += --enable-avalon
endif
ifeq ($(CONFIG_CGMINER_AVALON2),y)
	CONFIGURE_ARGS += --enable-avalon2
endif
ifeq ($(CONFIG_CGMINER_AVALON4),y)
	CONFIGURE_ARGS += --enable-avalon4
endif
ifeq ($(CONFIG_CGMINER_AVALON6),y)
	CONFIGURE_ARGS += --enable-avalon4
endif
ifeq ($(CONFIG_CGMINER_AVALON7),y)
	CONFIGURE_ARGS += --enable-avalon7 CFLAGS=-DSTRATUM_USER_AGENT=\\\"a7\\\"
endif
ifeq ($(CONFIG_CGMINER_AVALON8),y)
	CONFIGURE_ARGS += --enable-avalon8 CFLAGS=-DSTRATUM_USER_AGENT=\\\"a8\\\"
endif
ifeq ($(CONFIG_CGMINER_AVALON8_LP),y)
	CONFIGURE_ARGS += --enable-avalon8_lp CFLAGS=-DSTRATUM_USER_AGENT=\\\"a8\\\"
endif
ifeq ($(CONFIG_CGMINER_AVALON9),y)
	CONFIGURE_ARGS += --enable-avalon9 CFLAGS=-DSTRATUM_USER_AGENT=\\\"a9\\\"
endif
ifeq ($(CONFIG_CGMINER_AVALON911),y)
	CONFIGURE_ARGS += --enable-avalon9 CFLAGS=-DSTRATUM_USER_AGENT=\\\"a9\\\"
endif
ifeq ($(CONFIG_CGMINER_AVALONLC3),y)
	CONFIGURE_ARGS += --enable-avalonlc3 CFLAGS=-DSTRATUM_USER_AGENT=\\\"a9\\\"
endif

ifeq ($(CONFIG_TARGET_brcm2708_RaspberryPi),)
	CONFIGURE_ARGS += --without-curses
endif

define Build/Compile
	$(call Build/Compile/Default)
	(cd $(PKG_BUILD_DIR) && \
	 $(TARGET_CC) -Icompat/jansson-2.6/src `pkg-config --cflags libusb-1.0` api-example.c -o cgminer-api;)
endef

define Package/cgminer/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_DIR) $(1)/etc/config

	$(INSTALL_BIN) $(PKG_BUILD_DIR)/cgminer-api	   $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/cgminer  $(1)/usr/bin

ifeq ($(CONFIG_CGMINER_AVALON1),y)
	$(INSTALL_BIN) $(FILES_DIR)/cgminer-avalon1-monitor        $(1)/usr/bin/cgminer-monitor
	$(INSTALL_BIN) $(FILES_DIR)/cgminer.avalon1.init           $(1)/etc/init.d/cgminer
	$(CP)          $(FILES_DIR)/cgminer.avalon1.config         $(1)/etc/config/cgminer
endif

ifeq ($(CONFIG_CGMINER_AVALON2),y)
	$(INSTALL_BIN) $(FILES_DIR)/cgminer-avalon2-monitor        $(1)/usr/bin/cgminer-monitor
	$(INSTALL_BIN) $(FILES_DIR)/cgminer.avalon2.init           $(1)/etc/init.d/cgminer
	$(CP)          $(FILES_DIR)/cgminer.avalon2.config         $(1)/etc/config/cgminer
endif

ifeq ($(CONFIG_CGMINER_AVALON4),y)
	$(INSTALL_BIN) $(FILES_DIR)/cgminer-avalon4-monitor        $(1)/usr/bin/cgminer-monitor
	$(INSTALL_BIN) $(FILES_DIR)/cgminer.avalon4.init           $(1)/etc/init.d/cgminer
	$(CP)          $(FILES_DIR)/cgminer.avalon4.config         $(1)/etc/config/cgminer
	$(INSTALL_BIN)          $(FILES_DIR)/mm-avalon4-upgrade             $(1)/usr/bin/mmupgrade
endif
ifeq ($(CONFIG_CGMINER_AVALON6),y)
	$(INSTALL_BIN) $(FILES_DIR)/cgminer-avalon6-monitor        $(1)/usr/bin/cgminer-monitor
	$(INSTALL_BIN) $(FILES_DIR)/cgminer.avalon6.init           $(1)/etc/init.d/cgminer
	$(CP)          $(FILES_DIR)/cgminer.avalon6.config         $(1)/etc/config/cgminer
	$(INSTALL_BIN)          $(FILES_DIR)/mm-avalon6-upgrade             $(1)/usr/bin/mmupgrade
endif
ifeq ($(CONFIG_CGMINER_AVALON7),y)
	$(INSTALL_BIN) $(FILES_DIR)/cgminer-avalon7-monitor        $(1)/usr/bin/cgminer-monitor
	$(INSTALL_BIN) $(FILES_DIR)/cgminer.avalon7.init           $(1)/etc/init.d/cgminer
	$(CP)          $(FILES_DIR)/cgminer.avalon7.config         $(1)/etc/config/cgminer
	$(INSTALL_BIN)          $(FILES_DIR)/mm-avalon7-upgrade             $(1)/usr/bin/mmupgrade
endif
ifeq ($(CONFIG_CGMINER_AVALON8),y)
	$(INSTALL_BIN) $(FILES_DIR)/cgminer-avalon8-monitor        $(1)/usr/bin/cgminer-monitor
	$(INSTALL_BIN) $(FILES_DIR)/cgminer.avalon8.init           $(1)/etc/init.d/cgminer
	$(CP)          $(FILES_DIR)/cgminer.avalon8.config         $(1)/etc/config/cgminer
	$(INSTALL_BIN)          $(FILES_DIR)/mm-avalon8-upgrade             $(1)/usr/bin/mmupgrade
endif
ifeq ($(CONFIG_CGMINER_AVALON8_LP),y)
	$(INSTALL_BIN) $(FILES_DIR)/cgminer-avalon8-monitor        $(1)/usr/bin/cgminer-monitor
	$(INSTALL_BIN) $(FILES_DIR)/cgminer.avalon8.init           $(1)/etc/init.d/cgminer
	$(CP)          $(FILES_DIR)/cgminer.avalon8_lp.config      $(1)/etc/config/cgminer
	$(INSTALL_BIN)          $(FILES_DIR)/mm-avalon8-upgrade             $(1)/usr/bin/mmupgrade
endif
ifeq ($(CONFIG_CGMINER_AVALON9),y)
	$(INSTALL_BIN) $(FILES_DIR)/cgminer-avalon9-monitor        $(1)/usr/bin/cgminer-monitor
	$(INSTALL_BIN) $(FILES_DIR)/cgminer.avalon9.init           $(1)/etc/init.d/cgminer
	$(CP)          $(FILES_DIR)/cgminer.avalon9.config         $(1)/etc/config/cgminer
	$(INSTALL_BIN)          $(FILES_DIR)/mm-avalon9-upgrade             $(1)/usr/bin/mmupgrade
endif
ifeq ($(CONFIG_CGMINER_AVALON911),y)
	$(INSTALL_BIN) $(FILES_DIR)/cgminer-avalon9-monitor        $(1)/usr/bin/cgminer-monitor
	$(INSTALL_BIN) $(FILES_DIR)/cgminer.avalon9.init           $(1)/etc/init.d/cgminer
	$(CP)          $(FILES_DIR)/cgminer.avalon9.config         $(1)/etc/config/cgminer
	$(INSTALL_BIN)          $(FILES_DIR)/mm-avalon9-upgrade             $(1)/usr/bin/mmupgrade
endif
ifeq ($(CONFIG_CGMINER_AVALONLC3),y)
	$(INSTALL_BIN) $(FILES_DIR)/cgminer-avalonlc3-monitor        $(1)/usr/bin/cgminer-monitor
	$(INSTALL_BIN) $(FILES_DIR)/cgminer.avalonlc3.init           $(1)/etc/init.d/cgminer
	$(CP)          $(FILES_DIR)/cgminer.avalonlc3.config         $(1)/etc/config/cgminer
	$(INSTALL_BIN)          $(FILES_DIR)/mm-avalonlc3-upgrade             $(1)/usr/bin/mmupgrade
endif
endef

$(eval $(call BuildPackage,cgminer))
