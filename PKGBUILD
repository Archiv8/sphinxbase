#!/bin/bash

# Disable various shellcheck rules that produce false positives in this file.
# Repository rules should be added to the .shellcheckrc file located in the
# repository root directory, see https://github.com/koalaman/shellcheck/wiki
# and https://archiv8.github.io for further information.
# shellcheck disable=SC2034,SC2154
# [Query]: Latest release was, 5prealpha on 2016/09/24 and latest repository update was 2018/02/10. Is Sphinxbase project abandoned?
# [ToDo]: Add files: User documentation
# [ToDo]: Add files: Tooling
# [FixMe]: Package fails to build with configuration error:
#          configure: error: cannot import Python module "distutils".
#          Please check your Python installation. The error was:
#          <string>:1: DeprecationWarning: The distutils package is deprecated and slated for removal in Python 3.12. Use setuptools or check PEP 632 for 
#          potential alternatives
# [FixMe]: Namcap warnings and errors

# Maintainer: Ross Clark <archiv8@artisteducator.com>
# Contributor: Ross Clark <archiv8@artisteducator.com>

pkgname=sphinxbase
pkgver=5prealpha
pkgrel=12
pkgdesc="Common library for sphinx speech recognition"
url="http://cmusphinx.sourceforge.net/"
arch=("i686" "x86_64")
license=("BSD")
makedepends=(
  # Arch Linux dependencies
  "bison"
  "swig"
)
depends=(

  # Arch Linux dependencies
  "python"
  "lapack"
  "libpulse"
  # [Query]: Is "libsamplerate" needed
  "libsamplerate"
)
source=(
  "http://downloads.sourceforge.net/project/cmusphinx/${pkgname}/${pkgver}/${pkgname}-${pkgver}.tar.gz"
  "sphinxbase-5prealpha-fix-doxy2swig.patch")

sha512sums=(
  "9d999d0b9041c0965ff679636e3c5705987b70317a353916f447809a916878d831a82a5d9c1476d304f908df1ce6b68eb07c906af4f7b86ab84b859ee1b0d20b"
            "09c31a2fef4f63146c4f2b6440cb604392b16fc24f84679bce0a991541d7264082e281ae9f1d10bdf16701d3dc9e12166364243e14a1a65683fb7301ba2f8b1b")
options=("!libtool")

prepare() {
  cd "${pkgname}-${pkgver}"

  msg2 "Reconfiguring project for current version of Automake"
  autoreconf -ivf >/dev/null
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
