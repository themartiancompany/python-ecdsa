# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Angel Velasquez <angvp@archlinux.org>
# Maintainer: Felix Yan <felixonmars@archlinux.org>

_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_pkg=ecdsa
pkgname="${_py}-${_pkg}"
pkgver=0.19.0
pkgrel=2
pkgdesc="Implementation of ECDSA in Python"
arch=(
  'any'
)
_http="https://github.com"
_ns="tlsfuzzer"
url="${_http}/${_ns}/${pkgname}"
license=('MIT')
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
  "${_py}-six"
)
makedepends=(
  "${_py}-setuptools"
)
checkdepends=(
  "${_py}-pytest"
  "${_py}-hypothesis"
)
options=(
  !emptydirs
)
_pypi="https://files.pythonhosted.org/packages/source"
source=(
  "${_pypi}/${_pkg::0}/${_pkg}/${_pkg}-${pkgver}.tar.gz"
)
sha512sums=(
  '7fa90c810800f453ffcdf1872f9a8448cb6081478980cc3d7f282284b4e5483c3a86dc7b1ad6c3a4f46102479e9c8493a9d16903c462383ebf09f9021c0f3217'
)

prepare() {
  cd \
    "${_pkg}-${pkgver}"
}

check() {
  cd \
    "${_pkg}-${pkgver}"
  # https://github.com/tlsfuzzer/python-ecdsa/issues/336
  "${_py}" \
    -m \
      pytest \
    -k \
      'not test_implicit_unused_bits and not test_new_call_convention and not test_implicit_unexpected_unused and not test_new_call_convention'
}

package() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    setup.py \
      install \
        --root="${pkgdir}" \
	--optimize=1
  install \
    -Dm644 \
    LICENSE \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgname}/"
}
