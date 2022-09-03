# Maintainer: Frederik Schwan <freswa at archlinux dot org>
# Contributor: Honghao Li <im@rasphino.cn>

pkgname=sublime-merge-cracked
pkgver=2077
pkgrel=1
pkgdesc='Meet a new Git Client, from the makers of Sublime Text'
arch=('x86_64')
url='https://www.sublimemerge.com'
license=('custom')
depends=('gtk3')
conflicts=('sublime-merge')
source=("https://download.sublimetext.com/sublime-merge-${pkgver}-${pkgrel}-x86_64.pkg.tar.xz"
        LICENSE)
sha256sums=('36835e5d1612ead30fb48c71dc043dd7c5e48fd65f0f9d8546e7338fdc9f3c66'
            '7ba89459cc654c58bd1b3875b67daf6f6f672f86f3356dcc1165e29806ce136e')

package() {
  cd opt/sublime_merge

# === hack ===

      md5sum -c <<<"189196010502F17EB99A38D8F64163BA  sublime_merge" || exit
      echo 003CB652: 48 31 C0 C3             | xxd -r - sublime_merge 
      echo 003CE75D: 90 90 90 90 90          | xxd -r - sublime_merge 
      echo 003CE778: 90 90 90 90 90          | xxd -r - sublime_merge 
      echo 003CCC12: 48 31 C0 48 FF C0 C3    | xxd -r - sublime_merge 
      echo 003CB39E: C3                      | xxd -r - sublime_merge 
      echo 003CAFCE: C3                      | xxd -r - sublime_merge

# === hack end ==


  install -dm755 "${pkgdir}"/usr/bin

  # Install binaries
  install -Dm755 -t "${pkgdir}"/opt/sublime_merge/ \
    crash_reporter \
    git-credential-sublime \
    ssh-askpass-sublime \
    sublime_merge

  # link executable to /usr/bin/
  ln -s /opt/sublime_merge/sublime_merge "${pkgdir}"/usr/bin/smerge

  # copy misc files
  cp --preserve=mode -r -t "${pkgdir}"/opt/sublime_merge/ \
    changelog.txt \
    Packages \
    Icon

  # link app icons to system folder
  for res in 256x256 128x128 48x48 32x32 16x16; do
    install -dm755 "${pkgdir}"/usr/share/icons/hicolor/${res}/apps
    ln -s /opt/sublime_merge/Icon/${res}/sublime-merge.png "${pkgdir}"/usr/share/icons/hicolor/${res}/apps/sublime-merge.png
  done

  # install desktop file and license
  install -Dm644 -t "${pkgdir}"/usr/share/applications/ "${srcdir}"/usr/share/applications/sublime_merge.desktop
  install -Dm644 -t "${pkgdir}"/usr/share/licenses/${pkgname}/ "${srcdir}"/LICENSE
}
