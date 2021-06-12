# Copyright (C) 2020 Cascoda Ltd.

include $(TOPDIR)/rules.mk

PKG_NAME:=cascoda-sdk_miketest
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/Cascoda/cascoda-sdk.git
PKG_SOURCE_DATE:=2021-06-03
PKG_SOURCE_VERSION:=12ef831424f6f9fab692b3928e3d5bd5e92beb96

PKG_SOURCE:=$(PKG_NAME)-$(PKG_SOURCE_VERSION).tar.gz
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_SOURCE_VERSION)
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_SOURCE_VERSION)
PKG_MIRROR_HASH:=57803d9bca92818657b998dd4773523e4f42378e6442778bab041a8629351878

PKG_MAINTAINER:=Elie El Khoury <e.khoury@cascoda.com>, Ciaran Woodward <c.woodward@cascoda.com>

PKG_LICENSE:=BSD-3-Clause
PKG_LICENSE_FILES:=LICENSE

PKG_CHECK_FORMAT_SECURITY:=0

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/cascoda-sdk
  SECTION:=cascoda-sdk
  DEPENDS:=+libpthread +libstdcpp
  CATEGORY:=Utilities
  TITLE:=Cascoda utilities
endef

define Package/cascoda-sdk/description
  Cascoda Utilities: This package installs the following utilities

	ca-chillictl		- A Chili control application for listing and flashing connected Chili devices.
	ca-ot-eink-server	- A server that transmits image files, to be used with the ot-sed-eink-freertos embedded target. Requires a mac-dongle Chili to be connected to the host.
	ca-ot-sensordemo-server	- Interfaces with the Cascoda sensordemo application layer. It prints the sensor readings it receives from the network. Requires a mac-dongle Chili to be connected to the host.
	ca-serial-adapter	- A useful program for interacting with a serial application running on baremetal.
	ca-evbme-get		- Prints all the EVBME parameters of a connected Chili, including application name, version and joiner credentials. 
	ca-sniffer              - Captures raw 802.15.4 traffic. Compatible with WireShark. Requires a mac-dongle Chili to be connected to the host.
	ca-serial-test		- Stress test of the serial connection between the host and the connected Chili. Requires a Chili to be connected to the host.
	ca-stress-test		- Requires several mac-dongle Chilis to be connected to the host. Creates heavy 802.15.4 traffic.
	ca-security-test	- Tests the advanced security mode of the CA-8211.
	ca-rand-test		- No description yet.
	ca-ot-ncp-posix		- Enable a computer to act as a Thread Border Router. Requires a mac-dongle Chili to be connected to the host.
	ca-ot-cli-posix-ftd	- The OpenThread command line application, running on a host. Requires a mac-dongle Chili to be connected to the host.
	ca-ot-cli-posix-mtd	- Same as above, but acts as a Minimal Thread Device. Requires a mac-dongle Chili to be connected to the host.
	ca-ocfctl		- misssing!
endef

CMAKE_OPTIONS += -DBUILD_TESTING:Bool=OFF

define Build/Configure
  $(call Build/Configure/Default,--with-linux-headers=$(LINUX_DIR))
	sed -i '/MBEDTLS_HAVE_ASM/d' $(PKG_BUILD_DIR)/_deps/openthread-src/third_party/mbedtls/mbedtls-config.h
endef

define Package/cascoda-sdk/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_BUILD_DIR)/bin/chilictl $(1)/usr/bin/ca-chilictl
	$(CP) $(PKG_BUILD_DIR)/bin/ot-eink-server $(1)/usr/bin/ca-ot-eink-server
	$(CP) $(PKG_BUILD_DIR)/bin/ot-sensordemo-server $(1)/usr/bin/ca-ot-sensordemo-server
	$(CP) $(PKG_BUILD_DIR)/bin/serial-adapter $(1)/usr/bin/ca-serial-adapter
	$(CP) $(PKG_BUILD_DIR)/bin/sniffer $(1)/usr/bin/ca-sniffer
	$(CP) $(PKG_BUILD_DIR)/bin/evbme-get $(1)/usr/bin/ca-evbme-get
	$(CP) $(PKG_BUILD_DIR)/bin/test/rand-test $(1)/usr/bin/ca-rand-test
	$(CP) $(PKG_BUILD_DIR)/bin/test/stress-test $(1)/usr/bin/ca-stress-test
	$(CP) $(PKG_BUILD_DIR)/bin/test/security-test $(1)/usr/bin/ca-security-test
	$(CP) $(PKG_BUILD_DIR)/bin/test/serial-test $(1)/usr/bin/ca-serial-test
	$(CP) $(PKG_BUILD_DIR)/bin/ot-cli-posix-ftd $(1)/usr/bin/ca-ot-cli-posix-ftd
	$(CP) $(PKG_BUILD_DIR)/bin/ot-cli-posix-mtd $(1)/usr/bin/ca-ot-cli-posix-mtd
	$(CP) $(PKG_BUILD_DIR)/bin/ot-ncp-posix $(1)/usr/bin/ca-ot-ncp-posix
	$(CP) $(PKG_BUILD_DIR)/bin/ocfctl $(1)/usr/bin/ca-ocfctl
endef

$(eval $(call BuildPackage,cascoda-sdk))

