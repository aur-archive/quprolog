# Maintainer: perlawk

pkgname=quprolog
_pkgname=qp
pkgver=9.5
pkgrel=1
pkgdesc="Qu-Prolog is an extended Prolog designed primarily as a prototyping language and tactic language for interactive theorem provers. From the University of Queensland."
arch=('x86_64' 'i686')
url="http://itee.uq.edu.au/~pjr/HomePages/QuPrologHome.html"
license=('non-commercial')
depends=('rlwrap' 'python2')
install=qp.install
source=(
"http://itee.uq.edu.au/~pjr/HomePages/QPFiles/${_pkgname}${pkgver}.tar.gz"
)

build() {
	cd "${srcdir}"/${_pkgname}${pkgver}/
	./configure --prefix=/usr
	make -j4
}

package() {
	dest=/usr/share/qp
	cd "${srcdir}"/${_pkgname}${pkgver}/
	install -m755 -d "${pkgdir}"${dest}/bin
	install -m755 -d "${pkgdir}"${dest}/src
	install -m755 -d "${pkgdir}"${dest}/prolog/compiler
	install -m755 -d "${pkgdir}"${dest}/prolog/library
	install -m755 -d "${pkgdir}"${dest}/examples
	install -m755 -d "${pkgdir}"${dest}/doc/manual
	install -m755 -d "${pkgdir}"${dest}/doc/user
	install -m755 -d "${pkgdir}"/usr/share/man/man1
	install -m644 doc/man/man1/* "${pkgdir}"/usr/share/man/man1
	install -m755 bin/* "${pkgdir}"${dest}/bin
	rm -f "${pkgdir}"${dest}/bin/*.in
	rm -f "${pkgdir}"${dest}/bin/Makefile
	install -m644 examples/* "${pkgdir}"${dest}/examples
	install -m644 doc/manual/* "${pkgdir}"${dest}/doc/manual
	install -m644 doc/user/* "${pkgdir}"${dest}/doc/user
	install -m644 src/*h "${pkgdir}"${dest}/src
	install -m644 config.h "${pkgdir}"${dest}/

	install -m644 prolog/compiler/*q? "${pkgdir}"${dest}/prolog/compiler
	install -m644 prolog/library/*q?  "${pkgdir}"${dest}/prolog/library

	cd "$pkgdir${dest}/bin"
	sed -i "s!^libqofiles.*!libqofiles=\"${dest}/prolog/compiler/*.qo ${dest}/prolog/library/*.qo\"!" qc
	sed -i "s!swipl.*-F!swipl-x ${dest}/bin/qc1.boot.po -F!" qc1.boot
	sed -i "s!exec.*qx!exec qem -Q '${dest}/bin/qc1.qup.qx!" qc1.qup
	sed -i "s!-I.*!-I${dest}/src \$\*!" qcc
	sed -i "s!exec.*qx!exec qem -Q '${dest}/bin/qecat.qx!" qecat
	sed -i "s!exec.*qx!exec qem -Q '${dest}/bin/qg.qx!" qg
	sed -i "s!-f.*rl_commands!-f ${dest}/bin/rl_commands!g; s!-Q '.*qp.qx'!-Q '${dest}/bin/qp.qx'!g; s!exec.*qx!exec qem -Q '${dest}/bin/qp.qx!;" qp

}                                              
                                               
md5sums=('bc24430190944b4121d3c6a02b0ae038')
