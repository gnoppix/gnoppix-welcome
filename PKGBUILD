# Maintainer: Vladislav Nepogodin <nepogodin.vlad@gmail.com>

pkgname=gnoppix-hello
_pkgname=gnoppix-welcome
pkgver=0.15.4
pkgrel=1
pkgdesc='Welcome screen for Gnoppix'
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
sha512sums=('359a7681e64f01ec9d6bfd9269a0e9eeca6e50dfb0f988d153745388f4d10c64ca3c74ff908fb52044db374618edbc8976a5361a2c82d7af7586a405776cef30')
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

