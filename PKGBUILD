pkgname=('shotcut')
srcname='shotcut'
pkgdesc='Video editor'
pkgver='15.10'
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
provides=('shotcut')
conflicts=('shotcut')

source=(
    "${srcname}::git+https://github.com/mltframework/shotcut.git#tag=v${pkgver}"
    'shotcut.desktop'
    'melt.patch'
)
sha512sums=(
    'SKIP'
    'SKIP'
    'SKIP'
)

prepare() {
    cd "${srcdir}/${srcname}"

    git apply "${srcdir}/melt.patch"

    qmake PREFIX='/usr/'
}

build() {
    cd "${srcdir}/${srcname}"

    make
}

package() {
    cd "${srcdir}/${srcname}"

    make INSTALL_ROOT="${pkgdir}" install

    install -D --mode=644 "${srcdir}/shotcut.desktop" "${pkgdir}/usr/share/applications/shotcut.desktop"
}
