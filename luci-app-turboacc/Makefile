# SPDX-License-Identifier: GPL-3.0-only
#
# Copyright (C) 2023-2026 沉默の金 <cmzj@cmzj.org>
# Copyright (C) 2022 Lean <coolsnowwolf@gmail.com>
# Copyright (C) 2019-2022 ImmortalWrt.org

include $(TOPDIR)/rules.mk

PKG_NAME:=luci-app-turboacc
PKG_VERSION:=1.4
PKG_RELEASE:=1

PKG_LICENSE:=GPL-3.0-only
PKG_MAINTAINER:=chenmozhijin <cmzj11@gmail.com>

# 仅保留 BBR 和 FullCone 的配置感知
PKG_CONFIG_DEPENDS:= \
	CONFIG_PACKAGE_$(PKG_NAME)_INCLUDE_BBR_CCA \
	CONFIG_PACKAGE_$(PKG_NAME)_INCLUDE_NFT_FULLCONE

# 核心优化：彻底移除 SFE 核心包依赖，移除 +luci-compat 以实现纯 JS 架构
LUCI_TITLE:=LuCI support for Qualcomm NSS / BBR / Fullcone
LUCI_DEPENDS:= \
	+luci \
	+PACKAGE_$(PKG_NAME)_INCLUDE_BBR_CCA:kmod-tcp-bbr \
	+PACKAGE_$(PKG_NAME)_INCLUDE_NFT_FULLCONE:kmod-nft-fullcone
LUCI_PKGARCH:=all

# 清理 menuconfig 菜单，只保留你需要的核心功能开关
define Package/$(PKG_NAME)/config
config PACKAGE_$(PKG_NAME)_INCLUDE_BBR_CCA
	bool "Include BBR CCA"
	default y

config PACKAGE_$(PKG_NAME)_INCLUDE_NFT_FULLCONE
	bool "Include NFT FULLCONE"
	default y
endef

include $(TOPDIR)/feeds/luci/luci.mk

# call BuildPackage - OpenWrt buildroot signature
