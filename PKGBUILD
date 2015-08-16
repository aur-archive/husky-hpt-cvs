# Maintainer: x-demon
# Maintainer: Mantas M. <grawity@gmail.com>
pkgname=husky-hpt-cvs
pkgver=20120129
pkgrel=2
pkgdesc="Husky Portable Fidonet FTN tosser"
arch=('i686' 'x86_64')
url="http://husky.sourceforge.net/hpt.html"
license=('GPL2')
depends=('husky-areafix-cvs' 'husky-fidoconf-cvs' 'husky-huskylib-cvs')
provides=('husky-hpt' 'hpt')
options=('!libtool')

_cvsroot=":pserver:anonymous@husky.cvs.sourceforge.net:/cvsroot/husky"
_cvsmod="hpt"

build() {
	cd "$srcdir"

	msg "Performing source checkout..."
	if [ -d "$_cvsmod/CVS" ]; then
		cd "$_cvsmod"
		cvs -z3 update -d 
		cd ..
	else
		cvs -z3 -d "$_cvsroot" co -D "$pkgver" -f "$_cvsmod"
	fi
	msg "Source checkout finished."

	rm -rf "$_cvsmod-build"
	cp -r "$_cvsmod" "$_cvsmod-build"
	cd "$_cvsmod-build"

	cp huskymak.cfg "$srcdir"

	make
}

package() {
	cd "$srcdir/$_cvsmod-build"

	make DESTDIR="$pkgdir" install
}
