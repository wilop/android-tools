pkgname=android-tools
pkgver=35.0.2
pkgrel=1
pkgdesc='Android platform tools'
arch=(x86_64)
url='https://github.com/nmeum/android-tools'
license=(Apache MIT)
depends=(fmt protobuf brotli zstd pcre2 lz4)
makedepends=(googletest cmake go ninja git)
optdepends=('python: {mk,unpack_,repack_}bootimg and mkdtboimg support')
source=($url/releases/download/$pkgver/android-tools-$pkgver.tar.xz android-tools-35.0.2-fix.patch)
sha256sums=('d2c3222280315f36d8bfa5c02d7632b47e365bfe2e77e99a3564fb6576f04097'
            '56ff8d9328643b0cb1017ece2214cfba2d567bf2bd285bd28db56d0f77d34795'
  )

prepare(){
  cd android-tools-$pkgver
  patch -Np1 < ../android-tools-35.0.2-fix.patch
}

build() {
  cd android-tools-$pkgver
  cmake \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_CXX_FLAGS="$CXXFLAGS" \
    -DCMAKE_C_FLAGS="$CFLAGS" \
    -DCMAKE_FIND_PACKAGE_PREFER_CONFIG=ON \
    -Dprotobuf_MODULE_COMPATIBLE=ON \
    -DANDROID_TOOLS_LIBUSB_ENABLE_UDEV=ON \
    -DANDROID_TOOLS_USE_BUNDLED_LIBUSB=ON \
    -G Ninja -S . -B build
  cmake --build build
}

package() {
  cd android-tools-$pkgver

  DESTDIR="${pkgdir}" ninja -C build install
}
