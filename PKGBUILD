pkgname=python-pillow
pkgver=12.0.0
pkgrel=2
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
    'python-pybind11'
    'python-setuptools'
    'python-wheel'
    'tk'
)
source=(git+ssh://git@github.com/python-pillow/Pillow#tag=${pkgver})
sha256sums=(647812449e47570f976d08a0a80f78a8f22040001c9b19e3a490b2a8c3ceac39)

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
