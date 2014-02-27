#
# Copyright (C) 2006-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=dleyna-core
PKG_VERSION:=0.4.0
PKG_RELEASE=$(PKG_SOURCE_VERSION)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=git://github.com/01org/dleyna-core.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=46c830e2b4fb023a51d59b81792dffe22000faff
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz

PKG_FIXUP:=autoreconf
PKG_INSTALL=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/libdleyna-core
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Library for dealing with DLNA-related tasks
  URL:=http://www.gupnp.org/
  DEPENDS:=+glib2 +libgupnp
endef

define Package/libdleyna-core/description
  A small utility library that aims to ease the DLNA-related tasks such as media
  profile guessing, transcoding to a given profile, etc.
endef

TARGET_CFLAGS += $(FPIC)

define Build/Configure
	(cd $(PKG_BUILD_DIR); ./autogen.sh );
	$(call Build/Configure/Default)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/dleyna-1.0/libdleyna/core
	$(CP) $(PKG_INSTALL_DIR)/usr/include/dleyna-1.0/libdleyna/core/*.h $(1)/usr/include/dleyna-1.0/libdleyna/core/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libdleyna-core-1.0.{la,so*} $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/pkgconfig/*.pc \
		$(1)/usr/lib/pkgconfig
endef

define Package/libdleyna-core/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libdleyna-core-1.0.so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libdleyna-core))
