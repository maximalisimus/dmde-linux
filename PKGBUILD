# Maintainer: Mikhail Artamonov <maximalis171091@yandex.ru>
# makepkg --printsrcinfo > .SRCINFO && makepkg -scC --nocheck --skipchecksums --skipinteg --skippgpcheck

pkgbase=dmde-linux
pkgname=('dmde-linux' 'dmde-cli')
pkgver=4.0.6.806
pkgrel=1
pkgdesc="DMDE is a powerful tool for data searching, editing, and recovery on disks"
arch=('x86_64' 'i686')
_archi=$(uname -m)
url="https://dmde.ru/"
license=('custom')
makedepends=(unzip)
replaces=($pkgbase)

source_x86_64=("https://dmde.ru/download/dmde-4-0-6-806-lin64-gui.zip"
				"https://dmde.ru/download/dmde-4-0-6-806-lin64-con.zip")

source_i686=("https://dmde.ru/download/dmde-4-0-6-806-lin32-con.zip")

source=(dmde-linux.desktop
		dmde-cli.desktop
		logo.png
		dmde-start.sh)

sha512sums=('3a4718b824861ea8a72a93cc7ae66828e5160d3642331e1b8f1d299affcfdd71f32d521521abdceda6c31a58830e6808c815c1edb0eb77fda1b9d162223d1dc2'
			'1b6c947f0cf2ae001fe465031971b3b61fe79b7403ca1307f3693c4cc09b4a5c6698042b87fc95810f978ad152fa3edd46c5e22365b873e9b3959224f96ec2e1'
			'c32bbbb33b629b1953077fe9669a451c0adc308f94ce42c21e319ffe776695cb55c4d23831724186f966922a9fea073f8e65bb1f9a73afb5cb2e8075a0e5ebfe'
			'3ae42d333b768e0d761601a1bc8d85a785056e7a2a943394bee9be3de210c4033ceb5bf48660d2a13b0f67f9b54990c14db9d8fc6e18b462cbf95f496e95ff7a')

sha512sums_x86_64=('b2d20d13ced8780baa46a435c772af16b7b16b38c7daf65d2edc55f3560bb2ab417390ffd55cea6f424d4237ff911baa5547a45a9c9e279689fb1fd8fb82fc99'
					'1547997e6e60202468b024282955f251964b8827b9106f97300869f7e836c245a029bec35f9367a2cecd95c10ae5f461bf2c9ba2ff2934479ffdc4e8a38b080c')

sha512sums_i686=('6bcc41c8f853d71f3a53b9bb72136840fda74995ea995cd4647682bc3e398d8c3cecca02645f667fbeac7292412a673263fc5dc475147fe90c6a3f4d3f3af9ce')

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
