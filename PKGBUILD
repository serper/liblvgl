pkgname=liblvgl
pkgver=9.2.2
pkgrel=1
pkgdesc="LVGL Library"
arch=('x86_64')
url="https://lvgl.io"
license=('MIT')
depends=('mingw-w64-x86_64-ffmpeg')
makedepends=('mingw-w64-x86_64-cmake' 'mingw-w64-x86_64-pkg-config' 'mingw-w64-x86_64-git')
source=("https://github.com/lvgl/lvgl/archive/refs/tags/v$pkgver.tar.gz"
        "lv_conf.h"
        "fix-CMakeLists.txt.patch"
        "fix-custom.cmake.patch"
        "fix-lv_blend_neon.S.patch")
sha256sums=('SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP')

build() {
    cd "$srcdir"
    tar -xzf "lvgl-$pkgver.tar.gz"
    cp lv_conf.h "lvgl-$pkgver/"
    patch -p1 < fix-CMakeLists.txt.patch
    patch -p1 < fix-custom.cmake.patch
    patch -p1 < fix-lv_blend_neon.S.patch
    mkdir -p build
    cd build
    cmake -G "MSYS Makefiles" -DCMAKE_BUILD_TYPE=Release -DBUILD_SHARED_LIBS=ON -DCMAKE_INSTALL_PREFIX=/mingw64 -DLV_CONF_BUILD_DISABLE_DEMOS=0 -DLV_CONF_BUILD_DISABLE_EXAMPLES=0 ../lvgl-$pkgver
    make
}

package() {
    cd build
    make DESTDIR="$pkgdir" install
}