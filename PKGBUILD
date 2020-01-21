# Maintainer: Christoph Flick <christophflick@gmx.de>
pkgname=jmstoolbox
pkgver=5.6.0
pkgrel=1
pkgdesc="A \"Universal\" JMS Client able to interact with the greatest number of Queue Managers/Queue providers on the market in a consistent manner."
arch=('x86_64')
url="https://github.com/${pkgname}/${pkgname}"
license=('GPL3')
depends=('java-runtime>=11' 'gtk3')
makedepends=('maven' 'java-environment>=11')
install=
changelog=
source=("${pkgname}-${pkgver}.tar.gz"::"https://github.com/${pkgname}/${pkgname}/archive/v${pkgver}.tar.gz"
        "${pkgname}.sh")
sha256sums=('0f7d9f036af8dd3ea4b715617293d14b2246dbdf6d6af58650d0bd1971b94f03'
            '453d9d88c562066f659301fd3b9f9f9ba93ba2aaa40b417a15cca9f5d1db7854')

prepare() {
	cd "${pkgname}-${pkgver}"
    # Remove JRE inclusion as it is only needed for the windows build
    sed -i '17d' org.titou10.jtb.build/pom.xml
    sed -i '104d' org.titou10.jtb.product/pom.xml
}

build() {
	cd "${pkgname}-${pkgver}/org.titou10.jtb.build"
	mvn clean verify
}

#check() {
#	cd "$pkgname-$pkgver"
#	make -k check
#}

package() {
	cd "${pkgname}-${pkgver}/org.titou10.jtb.build/dist"
    tar -xf "${pkgname}-${pkgver}-linux.gtk.x86_64.tar.gz"

    # Install everything into /usr/lib/${pkgname}
    install -m 755 -d "${pkgdir}/usr/lib"
    cp -r "JMSToolBox" "${pkgdir}/usr/lib/${pkgname}"

    cd "${pkgdir}/usr/lib/${pkgname}"
    install -m 755 -d "${pkgdir}/usr/bin"
    install -m 755 "${srcdir}/${pkgname}.sh" "${pkgdir}/usr/bin/${pkgname}"
}
