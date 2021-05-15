# Maintainer: perigoso <perigoso@riseup.net>

pkgbase=bootsplash-themes
pkgname=('bootsplash-theme-arch')
pkgver=1
pkgrel=0
url="https://github.com/perigoso/bootsplash-arch"
arch=('aarch64')
license=('GPL')
makedepends=('git' 'imagemagick')
options=('!libtool' '!emptydirs')

source=("bootsplash-packer-git::git+https://gitlab.manjaro.org/manjaro-arm/packages/extra/bootsplash-packer.git"
	'bootsplash-arch.sh'
	'bootsplash-arch.initcpio_install'
	'spinner.gif'
	'archlogo.png'
	'packagekit-hide-bootsplash.service')

sha256sums=('SKIP'
            'e192539c7528838ceb8c716a4b707e253d5c3d9026c3b129719b1418ead3c78a'
            '79e06459ad41704871aa2965ac09bf7a2bbeae62db0c69a06bc219bccc80330b'
            'e3d7608144e6f7e0d13dcd51bea5dcc5d0729c4bd4110947ce75897a371490fc'
            '49889caf04862f3818130411e135f8c4ca757ec59c01f3a84bd7ad69d774b35b'
            '52586beb9cc92169cf17cfdb3039fe9d5422ee861d13931310593984be176adc')


build() {
  # Build bootsplash-packer first
  cd bootsplash-packer-git
  gcc $CFLAGS -o bootsplash-packer bootsplash-packer.c
  mv bootsplash-packer "$srcdir"
  cd "$srcdir"

  # Generate the splash image
  sh ./bootsplash-arch.sh
}

package_bootsplash-theme-arch() {
  pkgdesc="Bootsplash Theme with Arch logo"

  install -Dm644 "$srcdir/bootsplash-arch" "$pkgdir/usr/lib/firmware/bootsplash-themes/arch/bootsplash"
  install -Dm644 "$srcdir/bootsplash-arch.initcpio_install" "$pkgdir/usr/lib/initcpio/install/bootsplash-arch"

  install -Dm644 "$srcdir/packagekit-hide-bootsplash.service" "$pkgdir/usr/lib/systemd/system/packagekit-hide-bootsplash.service"
  mkdir -p "$pkgdir/usr/lib/systemd/system/system-update.target.wants"
  ln -s ../packagekit-hide-bootsplash.service "$pkgdir/usr/lib/systemd/system/system-update.target.wants/packagekit-hide-bootsplash.service"
}