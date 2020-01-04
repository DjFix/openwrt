#
# Copyright (C) 2012-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

ARCH:=arm
BOARD:=omapl138
BOARDNAME:=Presounus CS18AI
FEATURES:=usb usbgadget ext4 targz audio display nand squashfs
CPU_TYPE:=arm9
CPU_SUBTYPE:=ARM926EJ-S

KERNEL_PATCHVER:=4.14

MAINTAINER:=Roman Savrulin <romansavrulin@gmail.com>

KERNELNAME:=zImage dtbs

define Target/Description
	TI OMAP-L138 boards
endef

include $(INCLUDE_DIR)/target.mk

DEFAULT_PACKAGES += partx-utils mkf2fs e2fsprogs

$(eval $(call BuildTarget))
