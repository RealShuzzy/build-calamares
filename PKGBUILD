# Maintainer: Samir von Hansen samirvonhansen2016@gmail.com

_pkgname="calamares-shuzzyos"
pkgname="$_pkgname"
pkgver=3.4.0
pkgrel=1
pkgdesc="Distribution-independent installer framework"
url="https://github.com/RealShuzzy/calamares"
license=("GPL-3.0-or-later")
arch=('i686' 'x86_64')

depends=(
  'kcoreaddons'
  'kpmcore'
  'libpwquality'
  'qt6-declarative'
  'qt6-svg'
  'yaml-cpp'
)
makedepends=(
  'extra-cmake-modules'
  'ninja'
  'qt6-tools'
  'qt6-translations'
)

_pkgsrc="calamares"
_pkgext="tar.gz"
source=("$url/releases/download/archive/$_pkgname.$_pkgext")

sha256sums=('95f66a800fed8d16f846a03a92dd7a7b1d9c1a1018537773cfc9f8665ccf0e5a')

build() {
  local _skip_modules=(
    dracut
    dracutlukscfg
    dummycpp
    dummyprocess
    dummypython
    dummypythonqt
    initramfs
    initramfscfg
    interactiveterminal
    packagechooser
    packagechooserq
    services-openrc
  )

  local _cmake_options=(
    -B build
    -S "$_pkgsrc"
    -G Ninja
    -DCMAKE_BUILD_TYPE=Release
    -DCMAKE_INSTALL_PREFIX='/usr'
    -DCMAKE_INSTALL_LIBDIR='lib'
    -DWITH_QT6=ON
    -DINSTALL_CONFIG=ON
    -DSKIP_MODULES="${_skip_modules[*]}"
    -DBUILD_TESTING=OFF
    -Wno-dev
  )

  cmake "${_cmake_options[@]}"
  cmake --build build
}

package() {
  DESTDIR="$pkgdir" cmake --install build

  install -d "$pkgdir/etc/calamares"
  cp -r "../calamares/." "$pkgdir/etc/calamares/"
}