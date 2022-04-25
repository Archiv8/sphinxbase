#!/bin/bash

# Disable various shellcheck rules that produce false positives in this file.
# Repository rules should be added to the .shellcheckrc file located in the
# repository root directory, see https://github.com/koalaman/shellcheck/wiki
# and https://archiv8.github.io for further information.
# shellcheck disable=SC2034,SC2154
# ToDo: Add files: User documentation
# ToDo: Add files: Tooling
# FixMe: Namcap warnings and errors

# Maintainer: Ross Clark <archiv8@artisteducator.com>
# Contributor: Ross Clark <archiv8@artisteducator.com>


pkgname=sphinxbase
pkgver=5prealpha
pkgrel=12
pkgdesc='Common library for sphinx speech recognition'
url='http://cmusphinx.sourceforge.net/'
arch=('i686' 'x86_64')
license=('BSD')
makedepends=('bison' 'swig')
depends=('python' 'lapack' 'libpulse') # not sure if libsamplerate is needed 'libsamplerate'
source=("http://downloads.sourceforge.net/project/cmusphinx/${pkgname}/${pkgver}/${pkgname}-${pkgver}.tar.gz"
        "sphinxbase-5prealpha-fix-doxy2swig.patch")

sha256sums=('f72bdb59e50b558bed47cc2105777200d2b246a0f328e913de16a9b22f9a246f'
            '1cb485202f83dc517872f5ab41f59d18884af1b85799166d80e08860f7729919')
options=('!libtool')

prepare() {
  cd "${pkgname}-${pkgver}"

  msg2 "Reconfiguring project for current version of Automake"
  autoreconf -ivf > /dev/null
  patch -p1 -b -i ../sphinxbase-5prealpha-fix-doxy2swig.patch
}

build() {
  cd "${pkgname}-${pkgver}"

  export PYTHON=/usr/bin/python
  ./configure --prefix=/usr
  make
}

package() {
  cd "${pkgname}-${pkgver}"
  make DESTDIR="${pkgdir}/" install

  install -d "${pkgdir}/usr/share/licenses/${pkgname}"
  install -m644 "${srcdir}/${pkgname}-${pkgver}/LICENSE" \
                "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
