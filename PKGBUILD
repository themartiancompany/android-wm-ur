# SPDX-License-Identifier: AGPL-3.0

#    -----------------------------------------------------
#    Copyright © 2024, 2025, 2026  Pellegrino Prevete
#
#    All rights reserved
#    -----------------------------------------------------
#
#    This program is free software: you can redistribute
#    it and/or modify it under the terms of the
#    GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of
#    the License, or (at your option) any later version.
#
#    This program is distributed in the hope that it
#    will be useful, but WITHOUT ANY WARRANTY;
#    without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
#    See the GNU Affero General Public License for
#    more details.
#
#    You should have received a copy of the
#    GNU Affero General Public License
#    along with this program.
#    If not, see <https://www.gnu.org/licenses/>.

# Maintainers:
#   Truocolo
#     <truocolo@aol.com>
#     <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
#   Pellegrino Prevete (dvorak)
#     <pellegrinoprevete@gmail.com>
#     <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
# Contributors:
#   Mark Wagie
#     <mark dot wagie at proton dot me>
#   hexchain
#     <i@hexchain.org>

if [[ ! -v "_docs" ]]; then
  _docs="true"
fi
_py="python"
_proj=hip
_platform=android
_program=wm
_pkg=${_platform}-${_program}
pkgbase="${_pkg}"
pkgname=(
  "${pkgbase}"
)
if [[ "${_docs}" == "true" ]]; then
  pkgname+=(
    "${_pkg}-docs"
  )
fi
pkgver=0.0.1
_commit="bcb3001ec6e6115e2616b6e6a4a32fadf029e4cb"
_man_commit="024ef06be7873ef09e2f3896cba672f086229cd2"
pkgrel=8
_pkgdesc=(
  "Android Window Manager"
  "command-line program."
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  'any'
)
_http="https://github.com"
_ns="themartiancompany"
url="${_http}/${_ns}/${_pkg}"
license=(
  'Apache-2.0'
)
depends=(
  "android-activity-utils"
  "sudo"
  "termux-shortcuts-utils"
)
makedepends=(
  "make"
)
if [[ "${_docs}" == "true" ]]; then
  makedepends+=(
    "${_py}-docutils"
  )
fi
checkdepends=(
)
provides=(
  "${_program}"
)
_android_wm_docs_optdepends=(
  "${_pkg}-docs:"
    "Android Window Manager"
    "documentation"
    "and manuals."
)
_android_wm_wm_ref_optdepends+=(
 "${_pkg}:"
   "The package this documentation"
   "package pertains to."
)
optdepends=(
  "${_android_wm_docs_optdepends[*]}"
)
_tag_name="commit"
_tag="${_commit}"
_sum="e316c83989c6bdd564dd2f9770cdca4f06417db81eeffda24285df7498d46e93"
_sig_sum="SKIP"
_man_sum="0a2cc913186876293e1d8f62819b32b63162c5a60ebf3c9e2d356acba86f7da8"
_url="${url}"
if [[ "${_tag_name}" == "tag" ]]; then
  _archive_format="tar.gz"
  _url="${_url}/archive/refs/tags/v${_tag}.tar.gz"
  _man_url="${_url}-man/archive/refs/tags/v${_tag}.tar.gz"
elif [[ "${_tag_name}" == "commit" ]]; then
  _archive_format="zip"
  _uri="${_url}/archive/${_commit}.${_archive_format}"
  _man_uri="${_url}-man/archive/${_man_commit}.${_archive_format}"
fi
_tarname="${_pkg}-${_tag}"
_tarfile="${_tarname}.${_archive_format}"
_man_tarname="${_pkg}-man-${_man_commit}"
_man_tarfile="${_man_tarname}.${_archive_format}"
_src="${_tarfile}::${_uri}"
_man_src="${_man_tarfile}::${_man_uri}"
source=(
  "${_src}"
  "${_man_src}"
)
sha256sums=(
  "${_sum}"
  "${_man_sum}"
)

prepare() {
  rm \
    -vrf \
    "${srcdir}/${_tarname}/man"
  mv \
    "man-${_man_commit}" \
    "${srcdir}/${_tarname}/man"
}

package_android-wm() {
  local \
    _make_opts=()
  _make_opts+=(
    PREFIX="/usr"
    DESTDIR="${pkgdir}"
  )
  cd \
    "${_tarname}"
  make \
    "${_make_opts[@]}" \
    install-scripts
  install \
    -Dm644 \
    "COPYING" \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgname}/"
}

package_android-wm-docs() {
  local \
    _make_opts=()
  pkgdesc="${pkgdesc} (documentation)"
  depends=()
  optdepends=(
    "${_android_wm_ref_optdepends[*]}"
  )
  provides=()
  _make_opts+=(
    PREFIX="/usr"
    DESTDIR="${pkgdir}"
  )
  cd \
    "${_tarname}"
  make \
    "${_make_opts[@]}" \
    install-doc \
    install-man
  install \
    -Dm644 \
    "COPYING" \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgname}/"
}
