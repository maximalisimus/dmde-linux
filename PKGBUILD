# Maintainer: Mikhail Artamonov <maximalis171091@yandex.ru>
# makepkg --printsrcinfo > .SRCINFO && makepkg -scC --nocheck --skipchecksums --skipinteg --skippgpcheck

pkgbase=dmde-linux
pkgname=('dmde-linux' 'dmde-cli')
pkgver=4.2.0
pkgrel=1
pkgdesc="DMDE is a powerful tool for data searching, editing, and recovery on disks"
arch=('x86_64' 'i686')
_archi=$(uname -m)
url="https://dmde.ru/"
license=('custom')
makedepends=(unzip)
replaces=($pkgbase)

source_x86_64=("https://dmde.ru/download/dmde-4-2-0-814-lin64-gui.zip"
				"https://dmde.ru/download/dmde-4-2-0-814-lin64-con.zip")

source_i686=("https://dmde.ru/download/dmde-4-2-0-814-lin32-con.zip")

source=(dmde-linux.desktop
		dmde-cli.desktop
		logo.png
		dmde-start.sh)

sha512sums=('3a4718b824861ea8a72a93cc7ae66828e5160d3642331e1b8f1d299affcfdd71f32d521521abdceda6c31a58830e6808c815c1edb0eb77fda1b9d162223d1dc2'
			'1b6c947f0cf2ae001fe465031971b3b61fe79b7403ca1307f3693c4cc09b4a5c6698042b87fc95810f978ad152fa3edd46c5e22365b873e9b3959224f96ec2e1'
			'c32bbbb33b629b1953077fe9669a451c0adc308f94ce42c21e319ffe776695cb55c4d23831724186f966922a9fea073f8e65bb1f9a73afb5cb2e8075a0e5ebfe'
			'3ae42d333b768e0d761601a1bc8d85a785056e7a2a943394bee9be3de210c4033ceb5bf48660d2a13b0f67f9b54990c14db9d8fc6e18b462cbf95f496e95ff7a')

sha512sums_x86_64=('4827fed6a327984ce3e762fc35e4430956bdf6a253df6ff2b247646555bf67fdc88e797e2e5d10c85121a20965c7823105b86806d0003b224dd118ab3e4fc136'
					'f8c15f1146d8cae297ca775ef5e255706c4d79c2c23acaeba38851275ddd1de57411bf6e093dfb80c898b5e11afabb0f87f92b16082cec4b917574689b713772')

sha512sums_i686=('34b2208cb64a88131e64a9eb103345368c8c65e839c6da861959be4f84c07e4178f246f30c0c7e3829963c1bc9d9fc935ba88e78d667013bbabba157c1384f84')

package_dmde-cli() {
	replaces=("${pkgname[1]}")
	depends=(sudo)
	pkgdesc="DMDE is a powerful tool for data searching, editing, and recovery on disks - cli version"
	cd $srcdir
	if [[ "${_archi[*]}" == "x86_64" ]]; then
		_pkgname=$(basename "${source_x86_64[1]}")
	else
		_pkgname=$(basename "${source_i686[0]}")
	fi
	mkdir -p ./usr/share/dmde-cli/ $pkgdir/usr/bin/ $pkgdir/usr/share/applications/ $pkgdir/usr/share/pixmaps/
	rm -rf $srcdir/usr/share/dmde-linux/
	unzip "./${_pkgname[*]}" -d $srcdir/usr/share/dmde-cli/
	cp -r usr $pkgdir
	chmod +x $pkgdir/usr/share/dmde-cli/dmde
	chmod +x $pkgdir/usr/share/dmde-cli/dmde-su.sh
	install -vDm644 $srcdir/logo.png $pkgdir/usr/share/pixmaps/logo.png
	install -vDm644 "$srcdir/${pkgname[1]}.desktop" "$pkgdir/usr/share/applications/${pkgname[1]}.desktop"
	chmod +x "$pkgdir/usr/share/applications/${pkgname[1]}.desktop"
	ln -s /usr/share/dmde-cli/dmde $pkgdir/usr/bin/dmde-cli
}

package_dmde-linux() {
	replaces=("${pkgname[0]}")
	depends=(zenity sudo)
	pkgdesc="DMDE is a powerful tool for data searching, editing, and recovery on disks"
	cd $srcdir
	mkdir -p ./usr/share/dmde-linux/ $pkgdir/usr/bin/ $pkgdir/usr/share/applications/ $pkgdir/usr/share/pixmaps/
	_pkgname=$(basename "${source_x86_64[0]}")
	rm -rf $srcdir/usr/share/dmde-cli
	unzip "./${_pkgname[*]}" -d $srcdir/usr/share/dmde-linux/
	cp -r usr $pkgdir
	chmod +x $pkgdir/usr/share/dmde-linux/dmde
	chmod +x $pkgdir/usr/share/dmde-linux/dmde-su
	install -vDm644 $srcdir/logo.png $pkgdir/usr/share/pixmaps/logo.png
	install -vDm644 "$srcdir/${pkgname[0]}.desktop" "$pkgdir/usr/share/applications/${pkgname[0]}.desktop"
	chmod +x "$pkgdir/usr/share/applications/${pkgname[0]}.desktop"
	install -vDm644 $srcdir/dmde-start.sh $pkgdir/usr/share/dmde-linux/dmde-start.sh
	chmod +x $pkgdir/usr/share/dmde-linux/dmde-start.sh
	ln -s /usr/share/dmde-linux/dmde-start.sh $pkgdir/usr/bin/dmde
}
