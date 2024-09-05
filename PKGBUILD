# Maintainer: Andrei Korshikov <andrej.s.korshikov at gmail dot com>
# Contributor: Jaroslav Lichtblau <svetlemodry at archlinux dot org>
# Contributor: Ray Rashif <schiv at archlinux dot org>
# Contributor: Corrado Primier <bardo at aur dot archlinux dot org>
# Contributor: Vinay S Shastry <vinayshastry at gmail dot com>

pkgname='freemind-bin'
pkgver='1.0.1'
pkgrel=1
pkgdesc='A mind mapper, and a hierarchical editor with strong emphasis on folding'
arch=('any')
url='https://freemind.sourceforge.io/wiki/'
license=('GPL-2.0-or-later')
depends=('java-runtime<=11')
makedepends=('libicns')  # provides 'icns2png'
provides=('freemind')
conflicts=('freemind')
replaces=('freemind')    # remove on 01.01.2025
source=(
    "https://downloads.sourceforge.net/freemind/freemind-bin-max-${pkgver}.zip"
    'freemind.svg::https://sourceforge.net/p/freemind/code/ci/master/tree/freemind/images/76812-freemind_v0.4.svg?format=raw'
    'freemind.desktop'
    )
noextract=("freemind-bin-max-${pkgver}.zip")
b2sums=(
    '4e5b5f1ec41c48d00f70e246e67e66c0d606fba4d4f1cb5709957693d648446a2ee9ecd40d290dda627f65d25176eace5223abff405bcce7655d2604a4fc6e21'
    '2399111a45e6c0a6e88bcb612d2dbdbb1deecd0b034986a79303fef65c7608e350f47bffd0b45de21b019a87c4ff69b8ed09eca586bcd8ac03610fd376355b7a'
    'c1aeebe028d59c6d3c0f0c7ef5f4353ef08d7f7103944305cc3166d65b9ff593fd7c4eeea7f28e43ad887308fa45c334c91b81f75fc1b4f43f5d8dacb610b0b7'
    )

package() {
    install --directory "${pkgdir}/usr/share/freemind/"
    bsdtar --extract --file="freemind-bin-max-${pkgver}.zip" --directory="${pkgdir}/usr/share/freemind/"

    install --directory "${pkgdir}/usr/bin/"
    ln --symbolic '/usr/share/freemind/freemind.sh' "${pkgdir}/usr/bin/freemind"
    chmod +x "${pkgdir}/usr/share/freemind/freemind.sh"

    local _license_dir="${pkgdir}/usr/share/licenses/freemind/"
    install --directory "${_license_dir}"
    ln --symbolic "/usr/share/freemind/license" "${_license_dir}"

    local _prefix='FreeMindWindowIconModern'
    bsdtar --extract --file="${pkgdir}/usr/share/freemind/lib/freemind.jar" --include="images/${_prefix}.icns" --strip-components=1
    icns2png --extract "${_prefix}.icns"
    local _dots
    for _dots in 16 32 128 256 512
        do
            install -D --mode=644 "${_prefix}_${_dots}x${_dots}x32.png" "${pkgdir}/usr/share/icons/hicolor/${_dots}x${_dots}/apps/freemind.png"
        done
    install -D --mode=644 --target-directory="${pkgdir}/usr/share/icons/hicolor/scalable/apps/" 'freemind.svg'

    install -D --mode=644 --target-directory="${pkgdir}/usr/share/applications/" 'freemind.desktop'
    }
