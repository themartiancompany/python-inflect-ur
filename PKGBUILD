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

_os="$( \
  uname \
    -o)"
if [[ "${_os}" == "Android" ]]; then
  _build="false"
  _setuptools="true"
elif [[ "${_os}" == "GNU/Linux" ]]; then
  _build="true"
  _setuptools="false"
fi
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
  "${_py}-setuptools-scm"
  "${_py}-toml"
  "${_py}-wheel"
)
if [[ "${_build}" == "true" ]]; then
  makedepends+=(
    "${_py}-build"
    "${_py}-installer"
  )
elif [[ "${_setuptools}" == "true" ]]; then
  makedepends+=(
    "${_py}-setuptools"
  )
fi
checkdepends=(
  "${_py}-pytest"
  "${_py}-pytest-enabler"
)
_pypa="https://files.pythonhosted.org/packages/source"
source=(
  "${_pypa}/${_pkg::1}/${_pkg}/${_pkg}-${pkgver}.tar.gz"
)
sha512sums=(
  'ee9f69dff451017a2aad2226d8c6ae02b4b7b4bc4d4c49f3efee50d85eeef43c49c6c6ef3e7f30fa2c5ef21e065ff5242140d5a98bc71af17c7e70d9e75e54c1'
)
b2sums=(
  'a17c5cb5bfcd10530f29537335ffd1b4725fb1f53e78ef7ce1f40a3031fa486baae3400878e575c8ce6a77b4953332f051ec65dcba024a14c527301e51079edb'
)

if [[ "${_setuptools}" == "true" ]]; then
  source+=(
    'setup.py'
  )
  sha512sums+=(
    'c13481e9a7c96aca4412da449fa13342997a5eb2e70947e22cbd2d19ab6044d1d56c746b0acda2f830ea01701ebf55e2b93e9211fd6c91be73ba201d4b6bb3c8'
  )
  b2sums+=(
    '267cc44ad9d2c1f11287ab2a34d5fac160611bca1a0bdcf9b071f33584dd588d7024e5e4110485d07ef5fe3d9419a8c94a5ad1f59a7745e9cfb7efc952932668'
  )
fi

build() {
  cd \
    "${_pkg}-${pkgver}"
  if [[ "${_build}" == "true" ]]; then
    "${_py}" \
      -m build \
      --wheel \
      --no-isolation
  fi
}

check() {
  cd \
    "${_pkg}-${pkgver}"
  pytest \
    -vv
}

package() {
  cd \
    "${_pkg}-${pkgver}"
  if [[ "${_build}" == "true" ]]; then
  "${_py}" \
    -m installer \
    --destdir="${pkgdir}" \
    "dist/"*".whl"
  elif [[ "${_setuptools}" == "true" ]]; then
    cp \
      "${srcdir}/setup.py" \
      "."
    "${_py}" \
      "setup.py" \
      install \
      --root="${pkgdir}" \
      --optimize=1
  fi
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
