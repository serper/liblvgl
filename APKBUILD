# Contributor: Sergio Perez <3729853+serper@users.noreply.github.com>
# Maintainer: Sergio Perez <3729853+serper@users.noreply.github.com>
pkgname=lvgl-t113
pkgver=9.2.2
pkgrel=1
pkgdesc="LVGL Library for T113-S3"
url="https://lvgl.io"
arch="armv7"
license="MIT"
depends="libdrm libinput libxkbcommon ffmpeg-t113"
makedepends="cmake pkgconfig git ffmpeg-t113-dev libdrm-dev libinput-dev libxkbcommon-dev"
provides="lvgl=$pkgver-r$pkgrel"
replaces="lvgl"
subpackages="$pkgname-dev"
source="$pkgname-$pkgver.tar.gz::https://github.com/lvgl/lvgl/archive/refs/tags/v$pkgver.tar.gz
    lv_conf.h
    fix-CMakeLists.txt.patch
    fix-custom.cmake.patch
    fix-lv_blend_neon.S.patch
    "

prepare() {
    mv "$srcdir/lvgl-$pkgver" "$srcdir/$pkgname-$pkgver" || return 1
    default_prepare || return 1
    cp "$srcdir/lv_conf.h" "$srcdir/$pkgname-$pkgver"
}

build() {
    CMAKE_BUILD_PARALLEL_LEVEL=8 cmake -B build -S "$srcdir/$pkgname-$pkgver" \
        -DCMAKE_BUILD_TYPE=Release \
        -DBUILD_SHARED_LIBS=ON \
        -DCMAKE_INSTALL_PREFIX=/usr \
        -DLV_CONF_BUILD_DISABLE_DEMOS=0 \
        -DLV_CONF_BUILD_DISABLE_EXAMPLES=0 || return 1
    CMAKE_BUILD_PARALLEL_LEVEL=8 cmake --build build || return 1
}

package() {
    DESTDIR="$pkgdir" cmake --install build --prefix /usr || return 1
    install -Dm644 "$srcdir/$pkgname-$pkgver/lv_conf.h" "$pkgdir/usr/include/lv_conf.h" || return 1
}

dev() {
    default_dev
    provides="lvgl-dev=$pkgver-r$pkgrel"
    replaces="lvgl-dev"
}
sha512sums="
684571dcb279a60d6f36b86bd4e79e9f58d017708cd370eab8d832dc999f7502e37b8fdf9ba8432f7984dd220cdc8dae18fa22dd3fd59dea397f39c3d45f6834  lvgl-t113-9.2.2.tar.gz
a9bc8c1f3a9de813973bd74b650d0ef713e21537617976156191d91a010e3c3c6121accf555a6fd081a6345372ba96df79e2669d2a58d36ddf42b3f6ba96fe31  lv_conf.h
24c99f385b54641061269620112d603c0ed4d7435f693ec175961be51ac9efcadfbdb3b825da6b7ea5899f152c6603bddbc41899217bcd52d0d2717203c30497  fix-CMakeLists.txt.patch
a066d65dda681b050fc2b84582c5e83886368f6766aafbf2a8e4136113b8354e04b0b536956b46a440fb4a4e0e516e43504cef1762ee757e168c4c10a1c5fc24  fix-custom.cmake.patch
49afb77144944f2db21e3c0da483aee935bcff8016a5dd29b0ceea6630fa158a24f6efdb11fe98df10e8da15d253905f515c0e128106d4e96f8ae7ffa2edfe2f  fix-lv_blend_neon.S.patch
"
