# Maintainer: Deltachaos <mr@deltachaos.de>

pkgname=warcraftlogsuploader
_pkgapp=warcraftlogsuploader
pkgver=8.16.40
pkgrel=1
pkgdesc="warcraftlogs.com desktop client for Linux"
arch=('x86_64')
depends=("fuse2")
conflicts=("warcraftlogsuploader")
url="https://warcraftlogs.com/"
source=("${_pkgapp}-v8.16.40.AppImage::https://github.com/RPGLogs/Uploaders-warcraftlogs/releases/download/v8.16.40/warcraftlogs-v8.16.40.AppImage"
        'start')
license=('custom' 'MIT' 'custom:chromium-licenses')
options=(!strip)
# Skip checksum check for the WarcraftLogs binary, to avoid breakage on updates
sha512sums=('708eb1260da1fd093d16fb7c489e3e1943f7cfb9599d7861716589a004f1ce5185307d7413cd73794af240417d31242375b6f0fe96d301abd4e24b6be50b8c30'
            '1f8d504fb27e815f7efcc8e97672bad12f531d171ab8a08c49439fb4ee63b07e9355c49e56b5fb2eb2f6d202ce56a0526b609fef4b6209832026709002eba22a')

pkgver() {
    cd ${srcdir}
    chmod +x ${srcdir}/${_pkgapp}-v8.16.40.AppImage
    ${srcdir}/${_pkgapp}-v8.16.40.AppImage --appimage-extract >/dev/null
    cat ${srcdir}/squashfs-root/warcraftlogs.desktop | grep 'X-AppImage-Version' | sed 's!^X-AppImage-Version=!!g'
}

package() {
    cd ${srcdir}
    chmod +x ${srcdir}/${_pkgapp}-v8.16.40.AppImage
    ./${_pkgapp}-v8.16.40.AppImage --appimage-extract >/dev/null
    sed -i 's/Exec=.*/Exec=\/usr\/bin\/'${_pkgapp}' %U/' squashfs-root/warcraftlogs.desktop

    install -Dm755 ${_pkgapp}-v8.16.40.AppImage "${pkgdir}/opt/${_pkgapp}/${_pkgapp}.AppImage"
    install -Dm755 "start" "${pkgdir}/usr/bin/${_pkgapp}"
    install -dm755 "${pkgdir}/usr/share/applications/"
    install -dm755 "${pkgdir}/usr/share/icons/hicolor/512x512/apps/"
    install -dm755 "${pkgdir}/usr/share/licenses/${_pkgapp}/"

    cp --no-preserve=mode,ownership "${srcdir}/squashfs-root/warcraftlogs.desktop" "${pkgdir}/usr/share/applications/"
    for i in ${srcdir}/squashfs-root/LICENSE.* ${srcdir}/squashfs-root/LICENSES.*; do 
      cp --no-preserve=mode,ownership "${i}" "${pkgdir}/usr/share/licenses/${_pkgapp}"
    done
}
