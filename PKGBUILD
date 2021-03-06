# Maintainer: Chris Salzberg <chris@dejimata.com>
# Contributor: Leonidas Spyropoulos <artafinde@gmail.com>

pkgname=neomutt
pkgver=20170609
pkgrel=3
pkgdesc='The New Mutt: powerful text-based mail client with all the best feature patches'
url='http://www.neomutt.org/'
license=('GPL')
validpgpkeys=('86C2397270DD7A561263CA4E5FAF0A6EE7371805') # Richard Russon (flatcap) <rich@flatcap.org>
source=("https://github.com/neomutt/neomutt/archive/$pkgname-$pkgver.tar.gz"
        "https://github.com/neomutt/neomutt/releases/download/$pkgname-$pkgver/$pkgname-$pkgver.tar.gz.sig")
sha256sums=('feaaf7ac230cbf397f028fac5498e38b5d662078083e0cf3329ba04d1bb4b0cd'
            'SKIP')
arch=('i686' 'x86_64')
depends=('openssl' 'gdbm' 'mime-types' 'libsasl' 'gnupg' 'gpgme' 'libidn' 'krb5' 'notmuch-runtime')
optdepends=('urlview: for url menu')
makedepends=('git' 'gnupg' 'libxslt')
conflicts=('mutt')
provides=('mutt')

prepare() {
  cd $srcdir
  mv "$pkgname-neomutt-$pkgver" "$pkgname-$pkgver"
  cd "$pkgname-$pkgver"

  ./prepare \
    --prefix=/usr \
    --sysconfdir=/etc \
    --enable-debug \
    --enable-pgp \
    --enable-gpgme \
    --enable-notmuch \
    --with-gss=/usr \
    --with-ssl=/usr \
    --with-sasl \
    --with-curses=/usr \
    --with-regex \
    --with-idn \
    --with-gdbm
}

build() {
  cd "$pkgname-$pkgver"
  make
}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  # Install the program.
  make DESTDIR="$pkgdir" install
  # Cruft we don't want.
  rm "${pkgdir}"/etc/mime.types{,.dist}
}

# vim: ft=sh ts=2 sw=2 et
