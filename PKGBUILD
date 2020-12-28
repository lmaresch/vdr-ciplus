# This PKGBUILD is part of the VDR4Arch project [https://github.com/vdr4arch]
pkgname=vdr-ciplus
pkgver=1.0.2.r6.g55709fc
_gitver=55709fc63b6ef1a83a41e025bc1ba5fce1df3eeb
_vdrapi=2.4.6
pkgrel=2
pkgdesc="This plug-in is a feasibility study of an implementation of the CI Plus standard for VDR."
url="https://github.com/ciminus/vdr-plugin-ciplus"
arch=('x86_64')
license=('AGPL3')
depends=('openssl' "vdr-api=${_vdrapi}")
makedepends=('git')
_plugname=${pkgname//vdr-/}
source=("vdr-plugin-${_plugname}::git+https://github.com/ciminus/vdr-plugin-ciplus#commit=$_gitver"
        "50-$_plugname.conf")
backup=("etc/vdr/conf.avail/50-$_plugname.conf")
sha512sums=('SKIP'
         '26b09d53f5ff451d1ca708af4195e6b647c74bbf9e1836ffab3f8ad962cac5d210c616af28c05d07fd8f0850412c68bd177404856a6a3faad6ba26f8ca10729d')

pkgver() {
  cd "${srcdir}/vdr-plugin-$_plugname"
  _last_release=1.0.2
  _last_release_commit=baa77d4215cb02b7cb9259b8b53816626ce55634

  _count=$((`git rev-list --count HEAD` - `git rev-list --count $_last_release_commit`))
  if [ $_count -gt 0 ]; then
    printf "%s.r%s.g%s" $_last_release \
      $_count \
      `git rev-parse --short HEAD`
  else
    printf "%s" $_last_release
  fi
}

prepare() {
  cd "${srcdir}/vdr-plugin-${_plugname}"
}

build() {
  cd "${srcdir}/vdr-plugin-${_plugname}"
  make
}

package() {
  cd "${srcdir}/vdr-plugin-${_plugname}"
  make DESTDIR="${pkgdir}" install

  install -Dm644 "$srcdir/50-$_plugname.conf" "$pkgdir/etc/vdr/conf.avail/50-$_plugname.conf"
}
