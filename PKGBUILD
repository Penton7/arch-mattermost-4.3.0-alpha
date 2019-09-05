# Maintainer: William Gathoye <william at gathoye dot be>
# Maintainer: Aleksandar Trifunović <akstrfn at gmail dot com>
# Contributor: Jan Was <janek dot jan at gmail dot com>
# Contributor: Bruno Pagani <archange at archlinux dot org>
# Contributor: Tarasov Sergey <ontarget1212 at gmail dot com>

pkgname=mattermost-desktop
pkgver=4.3.0
pkgrel=3
pkgdesc="Mattermost Desktop application for Linux (Alpha)"
arch=('i686' 'x86_64')
url="https://github.com/mattermost/desktop"
license=('Apache')
depends=('electron4')
makedepends=('npm' 'git')
source=(
    "${pkgname}-${pkgver}.tar.gz"::"${url}/archive/v${pkgver}-rc0.tar.gz"
    "${pkgname}.sh"
    "${pkgname/-/.}"
)
sha512sums=('6d07f4d1fbdbb3d23e9eff5ef8b0ca643212b648afd6c61d12a87c92fd1c1b7336f2aeec36146fd177381fbcab7d18fa65023bee5169fe41b8ce09e457e84597'
            'ec10960a56593429996f153d0832345d1f9279aa386d5d09f078aed39a5e8e4c3d1900fc8ff608318c9c57a161c3850b2c7924d86af0ae41f76649c080fccc1f'
            'a8db88c1db7cba497ee2a1db059430d235942052322b26a2ece7a1340a28ae24686630fa89a37fcfa6bf9f277cbf8a7018ce78e7117b247b2b408fa0fb709d84'
            )


build() {
    cd "desktop-${pkgver}-rc0"
    npm install --cache "${srcdir}/npm-cache"
    npm run build --cache "${srcdir}/npm-cache"
}

package() {
    cd "desktop-${pkgver}-rc0"
    npm run package:linux --cache "${srcdir}/npm-cache"

    install -d "${pkgdir}/usr/lib"
    # The star in the unpackaged is needed for i686 or ARM platforms.
    cp -r release/linux*unpacked/resources "${pkgdir}/usr/lib/${pkgname}"

    install -Dm644 LICENSE.txt -t "${pkgdir}/usr/share/licenses/${pkgname}"
    install -Dm644 resources/linux/icon.svg "${pkgdir}/usr/share/icons/hicolor/scalable/apps/${pkgname}.svg"

    cd "${srcdir}"
    install -Dm755 ${pkgname}.sh "${pkgdir}/usr/bin/${pkgname}"
    install -Dm644 ${pkgname/-/.} -t "${pkgdir}/usr/share/applications/"
}
