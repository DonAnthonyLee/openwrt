#
# Copyright (C) 2007-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=mt7601u-ap
PKG_VERSION:=1.0.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/eywalink/mt7601u.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=cb1b0f3324b6dbf8f6a10276f5cb12382dc098e8
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz

include $(INCLUDE_DIR)/package.mk

define KernelPackage/mt7601u_ap
  SECTION:=sys
  CATEGORY:=Kernel modules
  SUBMENU:=Wireless Drivers
  TITLE:=Driver for MT7601U wireless adapters in AP mode
  FILES:=$(PKG_BUILD_DIR)/src/os/linux/rtutil7601Uap.ko $(PKG_BUILD_DIR)/src/os/linux/mt7601Uap.ko $(PKG_BUILD_DIR)/src/os/linux/rtnet7601Uap.ko
  DEPENDS:=@USB_SUPPORT
  AUTOLOAD:=$(call AutoProbe,\
	rtutil7601Uap \
	mt7601Uap \
	rtnet7601Uap)
endef

include $(INCLUDE_DIR)/kernel-defaults.mk

define KernelPackage/mt7601u_ap/description
  Driver for MT7601U wireless adapters in AP mode
endef

MT7601U_MAKEOPTS= -C $(PKG_BUILD_DIR) \
	KERNELRELEASE="$(LINUX_VERSION)" \
	TARGET="LINUX" \
	ARCH="$(LINUX_KARCH)" \
	PLATFORM="OPENWRT" \
	LINUX_SRC="$(KERNEL_BUILD_DIR)/linux-$(LINUX_VERSION)" \
	CROSS_COMPILE="$(KERNEL_CROSS)" \
	WIFI_MODE="AP"

define Build/Compile
	$(MAKE) $(MT7601U_MAKEOPTS)
endef

define KernelPackage/mt7601u_ap/conffiles
/etc/Wireless/RT2870AP/RT2870AP.dat
endef

define KernelPackage/mt7601u_ap/install
	$(INSTALL_DIR) $(1)/etc/Wireless/RT2870AP
	$(CP) $(PKG_BUILD_DIR)/etc/Wireless/RT2870AP/RT2870AP.dat $(1)/etc/Wireless/RT2870AP/
endef

$(eval $(call KernelPackage,mt7601u_ap))
