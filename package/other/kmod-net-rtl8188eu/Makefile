#
# Copyright (C) 2007-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=kmod-net-rtl8188eu
PKG_VERSION:=$(LINUX_VERSION)
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

EXTRA_KCONFIG:=\
	CONFIG_88EU_AP_MODE=y \
	CONFIG_R8188EU=m

include $(INCLUDE_DIR)/package.mk

define KernelPackage/net-rtl8188eu
  SECTION:=sys
  CATEGORY:=Kernel modules
  SUBMENU:=Wireless Drivers
  TITLE:=RTL8188EU support (staging)
  FILES:=$(PKG_BUILD_DIR)/r8188eu.ko
  DEPENDS:=@USB_SUPPORT +@DRIVER_WEXT_SUPPORT +kmod-cfg80211 +kmod-usb-core +rtl8188eu-firmware
  KCONFIG:=$(EXTRA_KCONFIG)
  AUTOLOAD:=$(call AutoProbe,r8188eu)
endef

include $(INCLUDE_DIR)/kernel-defaults.mk

define KernelPackage/net-rtl8188eu/description
  Driver for RTL8188EU wireless adapters
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	cp -af $(LINUX_DIR)/drivers/staging/rtl8188eu/* $(PKG_BUILD_DIR)/
	patch -p1 -d $(PKG_BUILD_DIR) < ./files/build.patch
endef

define Build/Compile
	$(KERNEL_MAKE) $(EXTRA_KCONFIG) SUBDIRS="$(PKG_BUILD_DIR)" modules
endef

$(eval $(call KernelPackage,net-rtl8188eu))
