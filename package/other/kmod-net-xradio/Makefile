#
# Copyright (C) 2007-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=kmod-net-xradio
PKG_VERSION:=svn144
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/fifteenhex/xradio.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=6bf0e2e21c80456e2a3d4ad1267caecde7165871
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz

EXTRA_KCONFIG:=\
        CONFIG_XRADIO=m

include $(INCLUDE_DIR)/package.mk

define KernelPackage/net-xradio
  SECTION:=sys
  CATEGORY:=Kernel modules
  SUBMENU:=Wireless Drivers
  TITLE:=Driver for XR819
  FILES:=$(PKG_BUILD_DIR)/xradio_wlan.ko
  DEPENDS:=+kmod-mac80211
  AUTOLOAD:=$(call AutoProbe,xradio_wlan)
endef

include $(INCLUDE_DIR)/kernel-defaults.mk

define KernelPackage/net-xradio/description
  Driver for XR819
endef

define Build/Compile
        $(KERNEL_MAKE) $(EXTRA_KCONFIG) SUBDIRS="$(PKG_BUILD_DIR)" modules
endef

$(eval $(call KernelPackage,net-xradio))
