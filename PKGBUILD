pkgname=android-tools
pkgver=36.0.1
pkgrel=1
pkgdesc='Android platform tools'
arch=(x86_64)
url='https://github.com/nmeum/android-tools'
license=(Apache MIT)
depends=(fmt protobuf brotli zstd pcre2 lz4)
makedepends=(googletest cmake go ninja git)
optdepends=('python: {mk,unpack_,repack_}bootimg and mkdtboimg support')
source=($url/releases/download/$pkgver/android-tools-$pkgver.tar.xz)
sha256sums=('38e8a84b739480141de0836bf6d581b3339ac7d53d0f7ce8c044a3368c8c2f8f')

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
