include $(TOPDIR)/rules.mk

PKG_NAME:=xc3sprog
PKG_REV:=742
PKG_VERSION:=r$(PKG_REV)
PKG_RELEASE:=1

PKG_SOURCE=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://svn.code.sf.net/p/xc3sprog/code/trunk
PKG_SOURCE_PROTO:=svn
PKG_SOURCE_VERSION=$(PKG_REV)
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/xc3sprog
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=xc3sporg
	URL:=http://xc3sprog.sourceforge.net/
	DEPENDS:=+libusb-compat +libftdi +libstdcpp
endef

define Package/xc3sprog/description
xc3sprog is a suite of utilities for programming Xilinx FPGAs, CPLDs, and EEPROMs with the Xilinx Parallel Cable and other JTAG adapters under Linux. 
endef

define Package/xc3sprog/install
	$(INSTALL_DIR) $(1)/usr/bin

	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/usr/bin/* \
		$(1)/usr/bin/

	$(CP) ./root-files/* $(1)/usr/bin
endef

$(eval $(call BuildPackage,xc3sprog))
