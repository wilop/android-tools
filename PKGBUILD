pkgname=android-tools
pkgver=37.0.0p1
pkgrel=1
pkgdesc='Android platform tools'
arch=(x86_64)
url='https://github.com/nmeum/android-tools'
license=(Apache MIT)
depends=(fmt protobuf brotli zstd pcre2 lz4)
makedepends=(googletest cmake go ninja git)
optdepends=('python: {mk,unpack_,repack_}bootimg and mkdtboimg support')
source=($url/releases/download/$pkgver/android-tools-$pkgver.tar.xz)
sha256sums=('2c6de1abe16b211c7d9f59276217e14fd9e0e18b20e331d3c84358f5dffd576e')

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
