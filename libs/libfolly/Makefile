include $(TOPDIR)/rules.mk

PKG_NAME:=libfolly
PKG_VERSION:=2019.09.09.00
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/facebook/folly/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=1aac1bb5c2e22fea68780734069ee73188523c5ede8cd210e3fa81a1ae56bfe0
PKG_BUILD_DIR:=$(BUILD_DIR)/folly-$(PKG_VERSION)

PKG_MAINTAINER:=Amol Bhave <ambhave@fb.com>
PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_PARALLEL:=1
CMAKE_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/libfolly
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=An open-source C++ library developed and used at Facebook.
  URL:=https://github.com/facebook/folly
  DEPENDS:=+boost +boost-context +boost-date_time +boost-filesystem +boost-program_options +boost-regex \
	+libopenssl +libdouble-conversion +libevent2 +glog +libsodium +libaio +libatomic \
	+libbz2 +zlib +libzstd +liblzma +liblz4 +PACKAGE_libunwind:libunwind
endef

define Package/libfolly/description
  An open-source C++ library developed and used at Facebook.
  Folly (acronymed loosely after Facebook Open Source Library) is a library of
  C++14 components designed with practicality and efficiency in mind.
  Folly contains a variety of core library components used extensively at Facebook.
  This package includes the shared library.
endef

CMAKE_OPTIONS += \
	-DCMAKE_POSITION_INDEPENDENT_CODE=ON \
	-DCXX_STD=c++14 \
	-DFOLLY_HAVE_UNALIGNED_ACCESS_EXITCODE=OFF \
	-DFOLLY_HAVE_UNALIGNED_ACCESS_EXITCODE__TRYRUN_OUTPUT=OFF \
	-DFOLLY_HAVE_LINUX_VDSO_EXITCODE=OFF \
	-DFOLLY_HAVE_LINUX_VDSO_EXITCODE__TRYRUN_OUTPUT=OFF \
	-DFOLLY_HAVE_WCHAR_SUPPORT_EXITCODE=OFF \
	-DFOLLY_HAVE_WCHAR_SUPPORT_EXITCODE__TRYRUN_OUTPUT=OFF \
	-DHAVE_VSNPRINTF_ERRORS_EXITCODE=OFF \
	-DHAVE_VSNPRINTF_ERRORS_EXITCODE__TRYRUN_OUTPUT=OFF \
	-DBUILD_SHARED_LIBS=ON

TARGET_CXXFLAGS += -ffunction-sections -fdata-sections -flto
TARGET_LDFLAGS += -Wl,--gc-sections,--as-needed

define Package/libfolly/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libfolly*.so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libfolly))
