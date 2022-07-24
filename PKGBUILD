# Maintainer: Quentin Bouvet <qbouvet at outlook dot com>
pkgname="anomaly"
pkgver=1.5.0.4.8
pkgrel=3
pkgdesc="S.T.A.L.K.E.R Anomaly - Wine package"
arch=('x86_64')
url="https://www.moddb.com/mods/stalker-anomaly"
license=('none')
depends=('wine' 'winetricks' 'unionfs-fuse')
makedepends=('rar2fs' 'libguestfs' 'innoextract') # 'fuse3-p7zip-git' 

#   https://www.reddit.com/r/stalker/
#     - Sidebar link
#         - https://drive.google.com/file/d/1bU6llckyOiAKxFqLO4FiDv-yIXeQk_AP
#   https://www.moddb.com/mods/stalker-anomaly/downloads
#     - Update 4
#     - Hotfix 8
source=(
  "manual://S.T.A.L.K.E.R. Anomaly 1.5.0.rar"
  "manual://Anomaly-150-8-Update-4.7z"
  "manual://Anomaly-150-8-Hotfix-8.1.7z"
  "manual://${pkgname}"                     # /usr/bin wrapper script
  "manual://${pkgname}-main.png"            # icon
  "manual://${pkgname}-launcher.desktop"    # shortcut
  "manual://${pkgname}-dx11.desktop"        # shortcut
)
sha256sums=(
  "d81cea0581ebd51274cc7074f92bbff6a669e74952b590052cac83470b741b56"
  "48eb6c3bc0a2eed47c963099b0cbc58ce761713b5489d845e2523d8139f7497f"
  "755d40a9828c5c663206052b2c764a3f700a8705d224c22c938d024a2ef5b35e"
  "2442ad4e0cd803428052c6812ec33448bd4e40da51c909e41851c239978dc4ee"
  "fcccac913fb8f770ff4547e1efcf7322f1bc4479e9c533664c3c67a0bea21095"
  "7c13c9a2901da62e01702abbff52132f7999ff9efdcdfbe59fe77bd661f5d8d9"
  "3935f451faedd31752ac07183eaa8051c96c021ad2238ac445651d5c28d5b26a"
)
noextract=(
  'S.T.A.L.K.E.R. Anomaly 1.5.0.rar'
  'Anomaly-150-8-Update-4.7z'
  'Anomaly-150-8-Hotfix-8.1.7z'
)
install="${pkgname}.install"


#prepare() {
#}


#build() {
#}


package() {
    cd "${srcdir}"    
    mkdir -p "${pkgdir}/usr/share/${pkgname}"
    
    # Extract to $pwd  
    # -ap: path within the archive
    pushd "${pkgdir}/usr/share/${pkgname}"
    unrar x \
      -ap'Anomaly 1.5 beta' \
      "${srcdir}/S.T.A.L.K.E.R. Anomaly 1.5.0.rar"
    popd 
    
    # -o: output directory
    # -ao: overwrite mode (a=all)
    7z x \
      -o"${pkgdir}/usr/share/${pkgname}/" \
      -ao'a' \
      'Anomaly-150-8-Update-4.7z'
    
    # -o: output directory
    # -ao: overwrite mode (a=all)
    7z x \
      -o"${pkgdir}/usr/share/${pkgname}/" \
      -ao'a' \
      'Anomaly-150-8-Hotfix-8.1.7z'
    
    #   Fix permissions
    find "$pkgdir"/usr/share -type f -exec chmod 644 "{}" \;
    find "$pkgdir"/usr/share -type d -exec chmod 755 "{}" \;
    
    #   Install binary wrapper
    install -m755 -D -t "${pkgdir}/usr/bin" "${pkgname}"
 
    #   Install Icon
    install -D -t "${pkgdir}/usr/share/icons/" \
      "${pkgname}-main.png"
      
    #   Install Desktop File
    install -D -t "${pkgdir}/usr/share/applications/" \
      "${pkgname}-launcher.desktop"
    install -D -t "${pkgdir}/usr/share/applications/" \
      "${pkgname}-dx11.desktop"
}

#
# makepkg --printsrcinfo > .SRCINFO
#
