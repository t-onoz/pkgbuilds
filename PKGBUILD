# shellcheck disable=SC2034,SC2154,SC2164
pkgname=('shotcut')
_srcname='shotcut'
pkgdesc='Video editor'
pkgver='18.06.02'
_commit='d06c470df30b17fdf90861726d6e1d7a52795e2c'
pkgrel='2'
arch=('i686' 'x86_64')
url='https://www.shotcut.org/'
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
    'movit'
    'ffmpeg'
    'libx264'
    'libvpx'
    'lame'
    'frei0r-plugins'
    'ladspa'
)
makedepends=('git' 'qt5-tools')
provides=("${pkgname[0]%-git}")
conflicts=("${pkgname[0]%-git}")

source=(
    "${_srcname}::git+https://github.com/mltframework/shotcut.git#commit=${_commit}"
    'shotcut.desktop'
    'melt.patch'
    'qt-5.11.patch'
)
sha512sums=(
    'SKIP'
    'SKIP'
    'SKIP'
    'SKIP'
)

prepare() {
    cd "${srcdir}/${_srcname}"

    git apply "${srcdir}/melt.patch"
    git apply "${srcdir}/qt-5.11.patch"
}

build() {
    cd "${srcdir}/${_srcname}"

    qmake PREFIX='/usr' \
        QMAKE_CFLAGS_RELEASE="${CFLAGS}" \
        QMAKE_CXXFLAGS_RELEASE="${CXXFLAGS}"
    make
}

package() {
    cd "${srcdir}/${_srcname}"

    make INSTALL_ROOT="${pkgdir}" install

    install -D --mode=644 "${srcdir}/shotcut.desktop" "${pkgdir}/usr/share/applications/shotcut.desktop"
}
