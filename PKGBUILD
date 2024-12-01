pkgname=liblvgl
pkgver=9.2.2
pkgrel=1
pkgdesc="LVGL Library"
arch=('x86_64')
url="https://lvgl.io"
license=('MIT')
depends=('mingw-w64-x86_64-ffmpeg')
makedepends=('mingw-w64-x86_64-cmake' 'mingw-w64-x86_64-pkg-config' 'mingw-w64-x86_64-tools-git')
source=("https://github.com/lvgl/lvgl/archive/refs/tags/v$pkgver.tar.gz"
        "lv_conf_win.h"
        "fix-CMakeLists.txt.patch"
        "fix-custom.cmake.patch"
        "fix-lv_blend_neon.S.patch")
sha256sums=('SKIP' 'SKIP' 'SKIP' 'SKIP' 'SKIP')

prepare() {
    cd "$srcdir/lvgl-$pkgver"
    cp "$srcdir/lv_conf_win.h" "lv_conf.h"
    patch -p1 < "$srcdir/fix-CMakeLists.txt.patch"
    patch -p1 < "$srcdir/fix-custom.cmake.patch"
    patch -p1 < "$srcdir/fix-lv_blend_neon.S.patch"
}

build() {
    cd "$srcdir/lvgl-$pkgver"
    mkdir -p build
    cd build
    cmake -G "MSYS Makefiles" -DCMAKE_BUILD_TYPE=Release -DBUILD_SHARED_LIBS=ON -DCMAKE_INSTALL_PREFIX=/mingw64 -DLV_CONF_BUILD_DISABLE_DEMOS=0 -DLV_CONF_BUILD_DISABLE_EXAMPLES=0 ..
    make
}

package() {
    cd "$srcdir/lvgl-$pkgver/build"
    make DESTDIR="$pkgdir" install
}