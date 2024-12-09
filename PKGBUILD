# Maintainer: Andreas Mueller amu@gnoppix.com>

pkgname=gnoppix-hello
_pkgname=gnoppix-welcome
pkgver=0.1.0
pkgrel=1
pkgdesc='Welcome screen for Gnoppix Linux'
arch=('x86_64')
groups=('gnoppix')
license=(GPL-3.0-or-later)
url="https://github.com/gnoppix/gnoppix-welcome"
depends=(
  glib2
  gtk3
  pciutils
  procps-ng
  qt6-tools
)
makedepends=(
  cargo
  clang
  clang
  git
  lld
  llvm
  meson
)
source=("${pkgname}-${pkgver}.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('b9d3727536c258d8f60303d7191eb81d4536a424e6ae57b128b5995b5c726f2828b224b4eb5789e4b2392b984dc7877c74f608ad13a25b49537057e6c5d2bb52')
provides=('gnoppix-hello')
conflicts=('gnoppix-hello')
options=(strip)

build() {
  cd "${srcdir}/${_pkgname}-${pkgver}"

  # Compile with clang
  export AR=llvm-ar
  export CC=clang
  export CXX=clang++
  export NM=llvm-nm
  export RANLIB=llvm-ranlib

  export RUSTFLAGS="-Cembed-bitcode -C opt-level=3 -Ccodegen-units=1 -Clinker=clang -C link-arg=-flto -Clink-arg=-fuse-ld=/usr/bin/ld.lld"

  meson setup --buildtype=release --prefix=/usr build
  meson compile -C build
}

package() {
  cd "${srcdir}/${_pkgname}-${pkgver}"/build

  # Compile with clang
  export AR=llvm-ar
  export CC=clang
  export CXX=clang++
  export NM=llvm-nm
  export RANLIB=llvm-ranlib

  export RUSTFLAGS="-Cembed-bitcode -C opt-level=3 -Ccodegen-units=1 -Clinker=clang -C link-arg=-flto -Clink-arg=-fuse-ld=/usr/bin/ld.lld"
  DESTDIR="${pkgdir}" meson install

  install -Dvm644 ../$pkgname.desktop \
    "$pkgdir/etc/skel/.config/autostart/$pkgname.desktop"
}

# vim:set sw=2 sts=2 et:
