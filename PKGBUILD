# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2024, 2025  Pellegrino Prevete
#
#    All rights reserved
#    ----------------------------------------------------------------------
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU Affero General Public License for more details.
#
#    You should have received a copy of the GNU Affero General Public License
#    along with this program.  If not, see <https://www.gnu.org/licenses/>.

# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: David Runge <dvzrv@archlinux.org>

_pkg=inflect
_py="python"
pkgname="${_py}-inflect"
pkgver=7.5.0
pkgrel=2
_pkgdesc=(
  "Correctly generate plurals,"
  "singular nouns, ordinals,"
  "indefinite articles"
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  'any'
)
_http="https://github.com"
_ns="jazzband"
url="${_http}${_ns}/${_pkg}"
license=(
  'MIT'
)
depends=(
 "${_py}"
 "${_py}-pydantic"
 "${_py}-typing-extensions"
)
makedepends=(
  "${_py}-build"
  "${_py}-installer"
  "${_py}-setuptools-scm"
  "${_py}-toml"
  "${_py}-wheel"
)
checkdepends=(
  "${_py}-pytest"
  "${_py}-pytest-enabler"
)
_pypa="https://files.pythonhosted.org/packages/source"
source=(
  "${_pypa}/${_pkg::1}/${_pkg}/${_pkg}-${pkgver}.tar.gz"
)
sha512sums=(
  '139ddfc73ce2f62e781eb2eefe1dc56d51e2af8380b23af1f542f63ec125921ce6cdacfcaf26b0221776ff83d9e4bea728df2dd58e3a2f25e32c6a5f0cc07d25'
)
b2sums=(
  '81f31bc89abd1d0d0b6f5774b5c83586dab68721f9a77394a3b6f5f0ba3380574e2261bbe7d2086503e6643b70a26e8d9efb46643660dc5125cf4ef9d5b8d8a3'
)

build() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m build \
    --wheel \
    --no-isolation
}

check() {
  cd \
    "${_pkg}-${pkgver}"
  pytest \
    -vv
}

package() {
  cd \
    $_name-$pkgver
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m installer \
    --destdir="${pkgdir}" \
    dist/*.whl
  install \
    -vDm 644 \
    {NEWS,README}.rst \
    -t \
      "${pkgdir}/usr/share/doc/${pkgname}"
  install \
    -vDm 644 \
    LICENSE \
    -t "${pkgdir}/usr/share/licenses/${pkgname}"
}

# vim:set sw=2 sts=-1 et:
