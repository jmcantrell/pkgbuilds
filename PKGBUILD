# Maintainer: Jeremy Cantrell <jmcantrell at gmail dot com>

pkgname=btrfs-snapshots-git
pkgver=0.1.1.r0.5b1a7ba
pkgrel=2
pkgdesc="Manage collections of btrfs snapshots"
arch=('any')
url="https://gitlab.com/jmcantrell/${pkgname%-git}"
license=('GPL3')
depends=('btrfs-progs')
makedepends=('git')
provides=("${pkgname%-git}")
conflicts=("${pkgname%-git}")
source=("git+$url.git")
md5sums=('SKIP')

pkgver() {
    cd "$srcdir/${pkgname%-git}"
    printf "%s" "$(git describe --long --tags | sed 's/^v//;s/\([^-]*-\)g/r\1/;s/-/./g')"
}

check() {
    cd "$srcdir/${pkgname%-git}"
    make -k check
}

prepare() {
    local file
    while read -r file; do
        sed -i "\:/usr/local/etc:s:/usr/local::g" "$file"
        sed -i "\:/usr/local:s:/usr/local:/usr:g" "$file"
    done < <(find "$srcdir/${pkgname%-git}" -type f)
}

package() {
    cd "$srcdir/${pkgname%-git}"
    INSTALL_ROOT=$pkgdir/usr make install
}
