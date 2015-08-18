# Contributor: Stefan Husmann <stefan-husmann@t-online.de>
pkgname=xiphos-webkit-svn
pkgver=4369
pkgrel=1
pkgdesc="A Bible study tool -- svn version from the webkit branch"
arch=('i686' 'x86_64')
url="http://xiphos.org"
license=('GPL')
depends=('libwebkit' 'libgsf' 'libglade' 'sword-svn')
makedepends=('gnome-common' 'gnome-doc-utils' 'intltool' 'subversion')
provides=('gnomesword' 'xiphos')
conflicts=('gnomesword' 'xiphos')
source=()
md5sums=()
install=xiphos-svn.install

_svntrunk=https://gnomesword.svn.sourceforge.net/svnroot/gnomesword/branches/webkit
_svnmod=xiphos

build() {
  cd "$srcdir"

  if [ -d $_svnmod/.svn ]; then
    (cd $_svnmod && svn up -r $pkgver)
  else
    svn co $_svntrunk --config-dir ./ -r $pkgver $_svnmod
  fi

  msg "SVN checkout done or server timeout"
  msg "Starting make..."

  rm -rf "$srcdir/$_svnmod-build"
  cp -r "$srcdir/$_svnmod" "$srcdir/$_svnmod-build"
  cd "$srcdir/$_svnmod-build"

  #
  # BUILD
  #
  
  sed -i 's+/usr/bin/env python+/usr/bin/env python2+' waf
  ./waf --prefix=/usr --backend=webkit --gtk=auto configure 
  ./waf --prefix=/usr --backend=webkit build 
  ./waf --destdir=$pkgdir --no-post-install install 
}
