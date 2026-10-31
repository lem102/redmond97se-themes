pkgbase=redmond97se-themes
pkgname=(
  obsidian-pure-icon-theme
  redmond97se-gtk-theme
  # redmond97se-metacity-theme
  # redmond97se-wine-theme
  redmond97se-xfwm4-theme
)
pkgver=2.13
pkgrel=1
pkgdesc='Redmond97-SE themes'
arch=('any')
url='https://codeberg.org/Sliver_X/Redmond97-SE'
license=('GPL3')
makedepends=(grep sed tar)
source=("https://codeberg.org/Sliver_X/Redmond97-SE/releases/download/v${pkgver}/Redmond97-SE_v${pkgver}.tar.xz")
sha256sums=('2f814c42abb654096be9e8238ec519cbb3749cf169b0f78e7cbec7474ae28a9b')

prepare() {
  find -type f -executable -exec chmod -x {} \;
}

package_obsidian-pure-icon-theme() {
  url='https://github.com/madmaxms/iconpack-obsidian'
  description='Faenza-based Obsidian Icon theme'
  conflicts=(obsidian-icon-theme)

  mkdir -p "${pkgdir}/usr/share/icons"
  tar -xf ./icons/Obsidian_Pure_v2.08.tar.xz -C "${pkgdir}/usr/share/icons"
  rm ./icons/Obsidian_Pure_v2.08.tar.xz
}

_package_subthemes() {
  subdir=$1

  echo "subtheme start"
  pwd

  tar -xf ./themes/themes-v2.13.tar.xz

  # for each theme
  # create a corresponding theme directory in /usr/share/themes if not already there
  # copy the "subdir" into that theme directory

  pushd themes

  for theme_directory in Redmond97*; do
      if [[ -e "$theme_directory/$subdir" ]]; then
          echo "loop"
          mkdir -p "${pkgdir}/usr/share/themes/${theme_directory}"
          cp -r "$theme_directory/$subdir" "${pkgdir}/usr/share/themes/${theme_directory}"
      fi
  done

  popd

  # declare -a sdirs
  # readarray -t sdirs < \
  #   <(find themes/{Old,New}/ -mindepth 3 -maxdepth 5 -name "${subdir}" -type d)
  # for sdir in "${sdirs[@]}"; do
  #   tdir="$(echo "${sdir}" | grep -o "/Redmond97 SE [^/]*/${subdir}\$")"
  #   mkdir -p "${pkgdir}/usr/share/themes/${tdir}"
  #   cp -a "${sdir}"/* "${pkgdir}/usr/share/themes/${tdir}/"
  #   #copy over index.theme for gtk theme only
  #   if [ "${sdir}" == "gtk-3.0" ]; then
  #     install -m0644 "${sdir}/../index.theme" "${pkgdir}/usr/share/themes/${tdir}/../"
  #   fi
  # done
}

package_redmond97se-gtk-theme() {
  pkgdesc='Redmond97-SE GTK and GNOME themes'
  optdepends=(obsidian-pure-icon-theme)
  _package_subthemes 'gtk-2.0'
  # _package_subthemes 'gtk-2.0-hidpi'
  _package_subthemes 'gtk-3.0'
  _package_subthemes 'gtk-4.0'
}

package_redmond97se-metacity-theme() {
  pkgdesc='Redmond97-SE Metacity themes'
  optdepends=(redmond97se-gtk-theme metacity)
  _package_subthemes metacity-1
}

package_redmond97se-wine-theme() {
  pkgdesc='Redmond97-SE WINE themes'
  optdepends=(redmond97se-gtk-theme wine)
  _package_subthemes wine
}

package_redmond97se-xfwm4-theme() {
  pkgdesc='Redmond97-SE XFWM4 themes'
  optdepends=(obsidian-pure-icon-theme redmond97se-gtk-theme xfwm4)
  _package_subthemes xfwm4
}

# vim:set ts=2 sw=2 et:
