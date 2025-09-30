pkgname=python-pillow
pkgver=11.3.0
pkgrel=1
pkgdesc='Python Imaging Library (PIL) fork'
arch=('x86_64')
url='https://pillow.readthedocs.io'
license=('MIT-CMU')
depends=(
    'freetype2'
    'glibc'
    'lcms2'
    'libavif'
    'libimagequant'
    'libjpeg-turbo'
    'libraqm'
    'libtiff'
    'libxcb'
    'openjpeg'
    'python'
    'python-packaging'
    'zlib'
)
makedepends=(
    'git'
    'libwebp'
    'python-build'
    'python-installer'
    'python-setuptools'
    'python-wheel'
    'tk'
)
source=(git+ssh://git@github.com/python-pillow/Pillow#tag=${pkgver})
sha256sums=(b27bbc2dd1581c13005c737f7951c218499744e5409209012fb811a810047001)

prepare() {
    cd Pillow

    # https://gitlab.archlinux.org/archlinux/packaging/packages/python-pillow/-/issues/3
    # Added has_feature_version
    git cherry-pick -n 54f4a346ef89e33eec0f889569a6d280eca70656

    # Updated tests for FreeType 2.14.1
    git cherry-pick -n 92e671d7970b8f96c50424c0c47efd0a1c95bc51
}

build() {
    cd Pillow

    python3 -m build --wheel --no-isolation
}

package() {
    cd Pillow

    python3 -m installer -d ${pkgdir} dist/*.whl

    local python_version=$(python3 -c 'import sys; print(".".join(map(str, sys.version_info[:2])))')
    install -vDm644 -t $pkgdir/usr/include/python${python_version} src/libImaging/*.h
}
