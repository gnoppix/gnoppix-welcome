# Maintainer: Vladislav Nepogodin <nepogodin.vlad@gmail.com>

pkgname=gnoppix-hello
_pkgname=Gnoppix-Welcome
pkgver=0.15.2
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
sha512sums=('4cad528290770a541822ab8f76ba219a613b96b9c51baaceaaa9c8fa0db278e19ca302ba46bfc7b2dbac57f87e97a23996dcfc4689ad59f234ee3a190ab76ade')
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
