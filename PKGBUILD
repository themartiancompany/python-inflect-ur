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
pkgver=7.0.0
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
  'b2ca39d0e36cda8c8c42d208443d3b84b10d659dcd0d368273503d6e76df19c61ac3c623d526ea918ca8b347d6db8bdfb691609e480eaa33dd4f1c37e008473b'
)
b2sums=(
  'ae896109acd33946e05902d121ecbd95e04dc33a1d6da6035148521de5baff8cff877a5c56c104bde29d56025e231e20f97e0ee50686de0ec19b567d53612314'
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
    --destdir="$pkgdir" \
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
