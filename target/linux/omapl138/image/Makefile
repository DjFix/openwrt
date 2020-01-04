#
# Copyright (C) 2012-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/image.mk

FAT32_BLOCK_SIZE=1024
FAT32_BLOCKS=$(shell echo $$(($(CONFIG_OMAPL138_USB_BOOT_PARTSIZE)*1024*1024/$(FAT32_BLOCK_SIZE))))

UBIFS_OPTS = -F -m 2048 -e 124KiB -c 4096 -U
UBI_OPTS = -m 2048 -p 128KiB -s 512 -O 2048

define Build/omapl138-usb
	rm -f $@.boot
	mkfs.fat $@.boot -C $(FAT32_BLOCKS)

#	mcopy -i $@.boot $(STAGING_DIR_IMAGE)/$(DEVICE_NAME)/MLO ::MLO
#	mcopy -i $@.boot $(STAGING_DIR_IMAGE)/$(DEVICE_NAME)/u-boot.img ::u-boot.img
#	mcopy -i $@.boot $(STAGING_DIR_IMAGE)/$(DEVICE_NAME)/uEnv.txt ::uEnv.txt
	mmd -i $@.boot ::/dtbs
	mcopy -i $@.boot $(LINUX_DIR)/../image-$(DEVICE_DTS).dtb ::/dtbs/$(DEVICE_DTS).dtb
	mcopy -i $@.boot $(IMAGE_KERNEL) ::/zImage
	./gen_omap_sdcard_img.sh $@ \
		$@.boot \
		$(IMAGE_ROOTFS) \
		$(OMAPL138_USB_BOOT_PARTSIZE) \
		$(CONFIG_TARGET_ROOTFS_PARTSIZE)
	rm -f $@.boot
endef

define Device/Default
  PROFILES := Default
  DEVICE_VARS :=
  KERNEL_NAME := zImage
  KERNEL := kernel-bin
  IMAGES := usb.img.gz
  IMAGE/usb.img.gz := omapl138-usb | append-metadata | gzip
  SUPPORTED_DEVICES = $(subst _,$(comma),$(1))
endef

define Device/presonus_cs18ai
  DEVICE_DTS_DIR := ../dts
  DEVICE_TITLE := Presonus CS18AI
  DEVICE_DTS := cs18ai
endef

TARGET_DEVICES += presonus_cs18ai

$(eval $(call BuildImage))
