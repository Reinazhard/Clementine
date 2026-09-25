# Maintainer: Fabio 'Lolix' Loli <fabio.loli@disroot.org> -> https://github.com/FabioLolix
# Contributor: zan <zan@420blaze.it>
# Contributor: Jacob Henner <code@ventricle.us>
# Contributor: Eduardo Sánchez Muñoz
# Contributor: Maxime Gauduin <alucryd@archlinux.org>
# Contributor: Stéphane Gaudreault <stephane@archlinux.org>
# Contributor: BlackEagle <ike.devolder@gmail.com>
# Contributor: Dany Martineau <dany.luc.martineau@gmail.com>

# Based on community/clementine PKGBUILD

pkgname=clementine-git
pkgver=1.4.1.r106.ga4b3599ec
pkgrel=3
pkgdesc='A modern music player and library organizer'
arch=(x86_64)
url="https://github.com/clementine-player/Clementine"
license=(GPL-3.0-or-later)
depends=(
    abseil-cpp
    alsa-lib
    chromaprint
    fftw
    glib2
    glibc
    gst-plugins-base-libs
    gstreamer
    hicolor-icon-theme
    libcdio
    libgcc
    libglvnd
    #libgpod
    #liblastfm-qt5 # removed from Arch repo
    #libmtp
    libpulse
    libstdc++
    libx11
    #projectm # now use bundled v4.x, Arch is at v3.x
    protobuf
    qt5-base
    qt5-x11extras
    sqlite
    taglib
    zlib
    )
makedepends=(
    boost
    cmake
    gettext
    git
    glu
    pkgconf
    qt5-tools
    #sparsehash
    )
optdepends=(
    'gst-plugins-base: "Base" plugin libraries'
    'gst-plugins-good: "Good" plugin libraries'
    'gst-plugins-bad: "Bad" plugin libraries'
    'gst-plugins-ugly: "Ugly" plugin libraries'
    'gst-libav: FFmpeg plugin'
    'gvfs: Various devices support'
    'udisks2: Removable device support'
    )
conflicts=(clementine)
provides=(clementine)
#options=(!lto)
source=("git+https://github.com/clementine-player/Clementine.git")
sha256sums=('SKIP')

pkgver() {
  git -C "$srcdir/Clementine" describe --tags --always |
    sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
  local _flags=(
    -DBUILD_WERROR=OFF
    -DCMAKE_BUILD_TYPE=Release
    -DENABLE_BOX=OFF
    -DENABLE_DROPBOX=OFF
    -DENABLE_FAST_MATH=OFF
    -DENABLE_GOOGLE_DRIVE=OFF
    -DENABLE_LIBGPOD=OFF
    -DENABLE_LIBLASTFM=OFF
    -DENABLE_LIBMTP=OFF
    -DENABLE_SEAFILE=OFF
    -DENABLE_SKYDRIVE=OFF
    -DENABLE_SPARKLE=OFF
    -DENABLE_WIIMOTEDEV=OFF
    -DUSE_SYSTEM_PROJECTM=OFF
    -DUSE_SYSTEM_TAGLIB=ON
  )

  cmake -B build -S "$srcdir/Clementine" -Wno-dev \
    -DCMAKE_INSTALL_PREFIX=/usr \
    "${_flags[@]}"

  cmake --build build
}

package() {
  DESTDIR="$pkgdir" cmake --install build
}
