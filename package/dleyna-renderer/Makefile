#
# Copyright (C) 2013 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=dleyna-renderer
PKG_VERSION:=0.4.0
PKG_RELEASE=$(PKG_SOURCE_VERSION)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=git://github.com/01org/dleyna-renderer.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=e9cae3c6e3a416d38a96cd884083ba8dc9fe5b34
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz

PKG_FIXUP:=autoreconf
PKG_INSTALL=1
PKG_REMOVE_FILES:=autogen.sh aclocal.m4

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/dleyna-renderer
  SECTION:=multimedia
  CATEGORY:=Multimedia
  DEPENDS:= +glib2 +libgssdp +libgupnp +libgupnp-av +libgupnp-dlna +libsoup +libdleyna-core
  TITLE:=A Headless UPnP Renderer
endef

define Package/dleyna-renderer/description
  dleyna-renderer implements the server component that provides UPnP
  controllers a means to render media content (audio, video and images)
  from a UPnP media server.
endef

CONFIGURE_ARGS+= \
	--with-build-cc="$(HOSTCC)" \
	--prefix="\usr"

define Package/dleyna-renderer/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/$(PKG_NAME)/libdleyna-renderer-1.0.so* $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/dleyna-renderer-service $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/etc/dleyna-renderer-service.conf $(1)/etc/
endef

$(eval $(call BuildPackage,dleyna-renderer))
