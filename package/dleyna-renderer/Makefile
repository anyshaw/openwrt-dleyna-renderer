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

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/dleyna-renderer
  SECTION:=multimedia
  CATEGORY:=Multimedia
  DEPENDS:=+gstreamer +glib2 +libgssdp +libgupnp +libgupnp-av +libgupnp-dlna +libsoup +libdleyna-core
  TITLE:=A Headless UPnP Renderer
endef

define Package/dleyna-renderer/description
  dleyna-renderer implements the server component that provides UPnP
  controllers a means to render media content (audio, video and images)
  from a UPnP media server.
endef

TARGET_LDFLAGS += \
	-Wl,-rpath-link=$(STAGING_DIR)/usr/lib

define Build/Configure
	(cd $(PKG_BUILD_DIR); ./autogen.sh );
	$(call Build/Configure/Default)
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		DESTDIR="$(PKG_INSTALL_DIR)" \
		all install
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/dleyna-1.0/libdleyna/renderer
	$(CP) $(PKG_INSTALL_DIR)/usr/include/dleyna-1.0/libdleyna/renderer/*.h $(1)/usr/include/dleyna-1.0/libdleyna/renderer/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/dleyna-renderer-service $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/$(PKG_NAME)
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/$(PKG_NAME)/libdleyna-renderer-1.0.{la,so*} $(1)/usr/lib/$(PKG_NAME)/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/lib/pkgconfig/*.pc \
		$(1)/usr/lib/pkgconfig
endef

define Package/dleyna-renderer/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/dleyna-renderer-service $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/$(PKG_NAME)
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/$(PKG_NAME)/libdleyna-renderer-1.0.so* $(1)/usr/lib/$(PKG_NAME)/
	$(INSTALL_DIR) $(1)/usr/share/dbus-1/services
	$(CP) $(PKG_INSTALL_DIR)/usr/share/dbus-1/services/*.service $(1)/usr/share/dbus-1/services/
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/etc/*.conf $(1)/etc/
endef

$(eval $(call BuildPackage,dleyna-renderer))
