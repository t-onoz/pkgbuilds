# shellcheck disable=SC2034,SC2154,SC2164
pkgname=('shotcut')
_srcname='shotcut'
pkgdesc='Video editor'
pkgver='16.11'
pkgrel='1'
arch=('i686' 'x86_64')
url='https://github.com/mltframework/shotcut'
license=('GPL3')

depends=(
    'qt5-base'
    'qt5-declarative'
    'qt5-graphicaleffects'
    'qt5-multimedia'
    'qt5-quickcontrols'
    'qt5-webkit'
    'qt5-websockets'
    'qt5-x11extras'
    'mlt'
    'ffmpeg'
    'libx264'
    'libvpx'
    'lame'
    'frei0r-plugins'
    'ladspa'
)
makedepends=('git')
provides=("${pkgname[0]%-git}")
conflicts=("${pkgname[0]%-git}")

source=(
    "${_srcname}::git+${url}.git#tag=v${pkgver}"
    'shotcut.desktop'
    'melt.patch'
)
sha512sums=(
    'SKIP'
    'SKIP'
    'SKIP'
)

prepare() {
    cd "${srcdir}/${_srcname}"

    git apply "${srcdir}/melt.patch"
}

build() {
    cd "${srcdir}/${_srcname}"

    qmake PREFIX='/usr/'
    make
}

package() {
    cd "${srcdir}/${_srcname}"

    make INSTALL_ROOT="${pkgdir}" install

    install -D --mode=644 "${srcdir}/shotcut.desktop" "${pkgdir}/usr/share/applications/shotcut.desktop"
}
