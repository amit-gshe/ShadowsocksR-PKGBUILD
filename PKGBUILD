# $Id$
# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: jiangxq <jiangxueqian at gmail dot com>
# Contributor: zh99998 <zh99998@gmail.com>
# Contributor: 4679kun <admin at 4679 dot us>

pkgname=shadowsocksr-libev
pkgver=2.4.0
_commit=5e194305e701d5f9a372a5c04a1ecd7e1802f37f
pkgrel=1
pkgdesc='A lightweight secured socks5 proxy for embedded devices and low end boxes'
arch=('i686' 'x86_64')
url='https://github.com/shadowsocks/shadowsocksr-libev'
license=('GPL3')
depends=('libcap' 'mbedtls' 'libsodium' 'libev' 'udns' 'pcre' 'libcorkipset')
makedepends=('git' 'asciidoc' 'xmlto')
install=${pkgname}.install
source=("git+https://github.com/shadowsocksr/shadowsocksr-libev.git#commit=$_commit"
        'shadowsocks-libev@.service'
        'shadowsocks-libev-server@.service'
        'shadowsocks-libev-redir@.service'
        'shadowsocks-libev-tunnel@.service')

sha512sums=('SKIP'
            '92186a3baf340e3e3b7e8893b01bbf29356d0111ea7ecc10bb6a31278a834a7c428c501b0bb15fc1e983c6dab74a7094deae2c5972a4b3e6807ece668944d321'
            '4e7d22145af1e2ac65bfa0d8883c3b30a6ac726728265a782519ab3912d6e3034861e19b411b54aa1cdbf999b1758584f6452d9c98afb72b71f3a0b215813317'
            'e233c0f67843509f542c25d6fc39fe6992571b7cd0ae75e3c9573a8cd6f9a72748b5c4d09914a6d9402bfe379db487c628b39c44cc165f71e48e874a56922b82'
            'b8de1cc489a1feb8c0ca59fef8abf6c524343483563462a167cb4a5bed5e9605fe76e4fdc71a248a8a5fc882032737a02747916f79043d50f850645067ed38eb')

build() {
  cd "$srcdir/$pkgname"
  sed -i 's|AC_CONFIG_FILES(\[libcork/Makefile libipset/Makefile\])||' configure.ac
  ./autogen.sh
  ./configure --prefix=/usr --enable-shared --enable-system-shared-lib
  make
}

package() {
  cd "$srcdir/$pkgname"
  make DESTDIR="$pkgdir/" install
  install -Dm644 "$srcdir/shadowsocks-libev@.service" "$pkgdir/usr/lib/systemd/system/shadowsocks-libev@.service"
  install -Dm644 "$srcdir/shadowsocks-libev-server@.service" "$pkgdir/usr/lib/systemd/system/shadowsocks-libev-server@.service"
  install -Dm644 "$srcdir/shadowsocks-libev-redir@.service" "$pkgdir/usr/lib/systemd/system/shadowsocks-libev-redir@.service"
  install -Dm644 "$srcdir/shadowsocks-libev-tunnel@.service" "$pkgdir/usr/lib/systemd/system/shadowsocks-libev-tunnel@.service"
}
