#
# Copyright (C) 2007-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=xradio-firmware
PKG_VERSION:=2017-10-07
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(KERNEL_BUILD_DIR)/$(PKG_NAME)-$(PKG_RELEASE)

PKG_FLAGS:=nonshared

include $(INCLUDE_DIR)/package.mk

XRADIO_FIRMWARE_URL:=@GITHUB/armbian/firmware/tree/master/xr819/
XRADIO_FIRMWARE_FILE:=$(PKG_NAME)-$(PKG_RELEASE)

define Package/xradio-firmware
  SECTION:=firmware
  CATEGORY:=Firmware
  DEPENDS:=
  TITLE:=firmware for XR819
endef

define Package/xradio-firmware/description
  Firmware for XR819
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	cp -f ./files/boot_xr819.bin $(PKG_BUILD_DIR)/boot_xr819.bin
	cp -f ./files/fw_xr819.bin $(PKG_BUILD_DIR)/fw_xr819.bin
endef

define Build/Compile
	true
endef

define Package/xradio-firmware/install
	$(INSTALL_DIR) $(1)/lib/firmware/xr819
	$(CP) $(PKG_BUILD_DIR)/*.bin $(1)/lib/firmware/xr819/
endef

$(eval $(call BuildPackage,xradio-firmware))
