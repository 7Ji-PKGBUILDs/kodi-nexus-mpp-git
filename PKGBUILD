# vim:set ts=2 sw=2 et:
# Maintainer: Faruk Dikcizgi <boogiepop@gmx.de>
# Contributor: graysky <therealgraysky AT protonmail DOT com>
# Contributor: BlackIkeEagle < ike DOT devolder AT gmail DOT com >
# Contributor: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: DonVla <donvla@users.sourceforge.net>
# Contributor: Ulf Winkelvos <ulf [at] winkelvos [dot] de>
# Contributor: Ralf Barth <archlinux dot org at haggy dot org>
# Contributor: B & monty - Thanks for your hints :)
# Contributor: marzoul
# Contributor: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Brad Fanella <bradfanella@archlinux.us>
# Contributor: [vEX] <niechift.dot.vex.at.gmail.dot.com>
# Contributor: Zeqadious <zeqadious.at.gmail.dot.com>
# Contributor: Bartłomiej Piotrowski <bpiotrowski@archlinux.org>
# Contributor: Maxime Gauduin <alucryd@gmail.com>
#
# Original credits go to Edgar Hucek <gimli at dark-green dot com>
# for his xbmc-vdpau-vdr PKGBUILD at https://archvdr.svn.sourceforge.net/svnroot/archvdr/trunk/archvdr/xbmc-vdpau-vdr/PKGBUILD

# set this to anything to build with clang rather than with gcc
_clangbuild=

pkgbase=kodi-nexus-mpp-git
pkgname=("$pkgbase" "$pkgbase-eventclients" "$pkgbase-tools-texturepacker" "$pkgbase-dev" "$pkgbase-ffmpegdirect")
pkgver=r62660.460db89710.0978cfe
pkgrel=1
arch=('aarch64' 'arm7f')
url="https://kodi.tv"
license=('GPL2')
makedepends=(
  'afpfs-ng' 'bluez-libs' 'cmake' 'curl' 'dav1d' 'doxygen' 'git' 'glew'
  'gperf' 'hicolor-icon-theme' 'java-runtime<21' 'libaacs' 'libass'
  'libbluray' 'libcdio' 'libcec' 'libgl' 'mariadb-libs' 'libmicrohttpd'
  'libmodplug' 'libmpeg2' 'libnfs' 'libplist' 'libpulse' 'libva'
  'libva-vdpau-driver' 'libxrandr' 'libxslt' 'lirc' 'lzo' 'mesa' 'nasm'
  'pcre' 'python-pycryptodomex' 'python-pillow' 'python-pybluez'
  'python-simplejson' 'shairplay' 'smbclient' 'taglib' 'tinyxml' 'swig'
  'upower' 'giflib' 'ghostscript' 'meson' 'gtest' 'graphviz'
  # wayland
  'wayland-protocols' 'waylandpp' 'libxkbcommon'
  # gbm
  'libinput' 'flatbuffers'
  # mpp
  'mpp-git' 'librga-multi'
)
options=(!lto strip !ccache)

[[ -n "$_clangbuild" ]] && makedepends+=('clang' 'lld' 'llvm')

_gitname=xbmc
_gitnameff='inputstream.ffmpegdirect'
_codename=Nexus

# Found on their respective github release pages. One can check them against
# what is pulled down when not specifying them in the cmake step.
# $CHROOT/build/kodi-git/src/kodi-build/build/download
#
# https://github.com/xbmc/FFmpeg/tags
# https://github.com/xbmc/libdvdcss/tags
# https://github.com/xbmc/libdvdnav/tags
# https://github.com/xbmc/libdvdread/tags
#
# fmt and crossguid can be found https://mirrors.kodi.tv/build-deps/sources/
#
_libdvdcss_version="1.4.3-Next-Nexus-Alpha2-2"
_libdvdnav_version="6.1.1-Next-Nexus-Alpha2-2"
_libdvdread_version="6.1.3-Next-Nexus-Alpha2-2"
_ffmpeg_version="4.4.1-Nexus-Alpha1"
_fmt_version="9.1.0"
_spdlog_version="1.10.0"
_crossguid_version="ca1bf4b810e2d188d04cb6286f957008ee1b7681"
_fstrcmp_version="0.7.D001"
_libudfread_version="1.1.2"
source=(
  "git+https://github.com/xbmc/xbmc.git#branch=$_codename"
  "git+https://github.com/xbmc/inputstream.ffmpegdirect.git#branch=$_codename"
  "git+https://github.com/xbmc/repo-binary-addons.git#branch=$_codename"
  "libdvdcss-$_libdvdcss_version.tar.gz::https://github.com/xbmc/libdvdcss/archive/$_libdvdcss_version.tar.gz"
  "libdvdnav-$_libdvdnav_version.tar.gz::https://github.com/xbmc/libdvdnav/archive/$_libdvdnav_version.tar.gz"
  "libdvdread-$_libdvdread_version.tar.gz::https://github.com/xbmc/libdvdread/archive/$_libdvdread_version.tar.gz"
  "ffmpeg-$_ffmpeg_version.tar.gz::https://github.com/xbmc/FFmpeg/archive/$_ffmpeg_version.tar.gz"
  "https://mirrors.kodi.tv/build-deps/sources/fmt-$_fmt_version.tar.gz"
  "https://mirrors.kodi.tv/build-deps/sources/spdlog-$_spdlog_version.tar.gz"
  "https://mirrors.kodi.tv/build-deps/sources/crossguid-$_crossguid_version.tar.gz"
  "https://mirrors.kodi.tv/build-deps/sources/fstrcmp-$_fstrcmp_version.tar.gz"
  "https://mirrors.kodi.tv/build-deps/sources/libudfread-$_libudfread_version.tar.gz"
  0001-ffmpeg-buildsys.patch
  0002-rkmpp-4.patch
  0003-ffmpegdirect-buildsys.patch
)

noextract=(
  "libdvdcss-$_libdvdcss_version.tar.gz"
  "libdvdnav-$_libdvdnav_version.tar.gz"
  "libdvdread-$_libdvdread_version.tar.gz"
  "ffmpeg-$_ffmpeg_version.tar.gz"
  "fmt-$_fmt_version.tar.gz"
  "spdlog-$_spdlog_version.tar.gz"
  "crossguid-$_crossguid_version.tar.gz"
  "fstrcmp-$_fstrcmp_version.tar.gz"
  "libudfread-$_libudfread_version.tar.gz"
)

b2sums=('SKIP'
        'SKIP'
        'SKIP'
        '2f503d3ab767094958f7ec10b4ad11ffd02665deee571c8f3c739bef5fc7e2ff84babc5a3fdee638dc095f896b72fe3ce65e6b688674cb5f7b7b77190992688c'
        'db4d05836d8fbb3637ae50bdbfc0e4b612ee6b3be24addfea94ce772c3bf28d58b63a3f252d6f9f016f72f8cbb841cc1820b091226b136f4c4664385a32da73c'
        'c94feb5a03a12efa5b7767965118d2500a088299ea36f3b82e46d157e45893e6b04503cb50f179ca681bac914457607fab26acfa6e304752b355c407578572d1'
        '51d310e7000aeba657d55341c5fdb540474e197b85062228ab4b314c8309ec11985aa7f105193333fc6106529e8e58c86eafe268190894be8532d0e0b9065fa6'
        'ff1daa43140615b63aeb1ecd0aa1c32d24decfd5006805080293ef3db04d544c0445a30e8da0d985a6f5a25ad48ce4f6ae61e52da5ea4a4d3b031c212da38b18'
        'e40afa9fd1dd791e1f703392f0f54fc798ed70537a9f1ee9c8598dd449f4cd4dd03bc4ce95e416cbbe224711a17e70708a106f0432384542d6316cf232cf8757'
        '0f78a8ab5a420297f666b3b8156d499a9141ec25c049d4d2bb2ba594dc585abe211a149b83c605cce4f5530207231a065d5f3a87a0c969781de8c6381afa2527'
        'a8b68fcb8613f0d30e5ff7b862b37408472162585ca71cdff328e3299ff50476fd265467bbd77b352b22bb88c590969044f74d91c5468475504568fd269fa69e'
        '1801d84a0ca38410a78f23e7d44f37e6d53346753c853df2e7380d259ce1ae7f0c712825b95a5753ad0bc6360cfffe1888b9e7bc30da8b84549e0f1198248f61'
        'a4c52a1efe8957c2d941a47caeb1b3ec86741d902ae2c58eff4aaba369475e72257bf63c43a1b5f55fc8d07bb2d0c5ea0b7717a028278eae6a34f5a91eb5047f'
        '80a1ad491bd89b4d90a91372117a37abee040f8bf606fa6662dda2d99cdbb0e78a6be8b79dcd315a6bbd0b6efa42d0d39a30270f073eaaed16892a1cf6c1965f'
        '943d358b4c127b77a691886a48245604081e3fdb5f05cd9a9821b52acf46bc6736089348f3299e00f35bbc09ba501d136088d96c7f118b3f5f3fe1cb7d77c7fd')

pkgver() {
  cd "$_gitname"
  local _kcommits="$(git rev-list --count HEAD)"
  local _kcommit="$(git rev-parse --short HEAD)"
  cd "../$_gitnameff"
  local _ffcommits="$(git rev-list --count HEAD)"
  local _ffcommit="$(git rev-parse --short HEAD)"
  local _revnum=$(($_kcommits + $_ffcommits))
  printf "r${_revnum}.${_kcommit}.${_ffcommit}"
}

prepare() {
  # use our local source, no network access should be allowed during build()
  sed -i "s|https://github.com/xbmc/repo-binary-addons.git $_codename|file://${srcdir}/repo-binary-addons/.git makepkg|" xbmc/cmake/addons/bootstrap/repositories/binary-addons.txt
  [[ -d kodi-build ]] && rm -rf kodi-build
  mkdir -p "$srcdir/kodi-build"
  [[ -d ffdirect-build ]] && rm -rf ffdirect-build
  mkdir -p "$srcdir/ffdirect-build"
  # when built with debug enabled LTO needs more than 2gb size which larger than /tmp ond efault arch
  # we are creating a temporary tmp folder to satisfy LTO, otherwise linking stage will fail
  mkdir -p "$srcdir/tmp"

  cd "$_gitname"
  patch -p1 -N -i ../0001-ffmpeg-buildsys.patch 
  cp ../0002-rkmpp-4.patch tools/depends/target/ffmpeg
  
  cd ../"$_gitnameff"
  patch -p1 -N -i ../0003-ffmpegdirect-buildsys.patch 
  rm -rf depends/common/ffmpeg

  if [[ -n "$_clangbuild" ]]; then
    msg "Building with clang"
    export CC=clang CXX=clang++
  fi
}

build() {
  cd "$srcdir/kodi-build"

  _args=(
    -DCMAKE_BUILD_TYPE=Release
    -DCMAKE_INSTALL_PREFIX=/usr
    -DCMAKE_INSTALL_LIBDIR=/usr/lib
    -DUSE_LTO=$(nproc)
    -DVERBOSE=ON
    -DENABLE_LDGOLD=OFF
    -DENABLE_EVENTCLIENTS=ON
    -DENABLE_INTERNAL_FFMPEG=ON
    -DENABLE_INTERNAL_FMT=ON
    -DENABLE_INTERNAL_SPDLOG=ON
    -DENABLE_INTERNAL_CROSSGUID=ON
    -DENABLE_INTERNAL_FSTRCMP=ON
    -DENABLE_INTERNAL_UDFREAD=ON
    -DENABLE_MYSQLCLIENT=ON
    -DENABLE_VAAPI=ON
    -DENABLE_VDPAU=ON
    -Dlibdvdcss_URL="$srcdir/libdvdcss-$_libdvdcss_version.tar.gz"
    -Dlibdvdnav_URL="$srcdir/libdvdnav-$_libdvdnav_version.tar.gz"
    -Dlibdvdread_URL="$srcdir/libdvdread-$_libdvdread_version.tar.gz"
    -DFFMPEG_URL="$srcdir/ffmpeg-$_ffmpeg_version.tar.gz"
    -DFMT_URL="$srcdir/fmt-$_fmt_version.tar.gz"
    -DSPDLOG_URL="$srcdir/spdlog-$_spdlog_version.tar.gz"
    -DCROSSGUID_URL="$srcdir/crossguid-$_crossguid_version.tar.gz"
    -DFSTRCMP_URL="$srcdir/fstrcmp-$_fstrcmp_version.tar.gz"
    -DUDFREAD_URL="$srcdir/libudfread-$_libudfread_version.tar.gz"
    -DAPP_RENDER_SYSTEM=gles
  )

  # https://github.com/google/flatbuffers/issues/7404
  CXXFLAGS+=' -Wno-error=restrict'

  echo "building kodi"
  cmake "${_args[@]}" ../"$_gitname"
  TMPDIR="$srcdir/tmp" make -j$(nproc)
  
  cd "$srcdir/ffdirect-build"
  echo "building ffmpeg-direct"
  cmake -DCMAKE_INSTALL_PREFIX=/usr \
        -DCMAKE_INSTALL_LIBDIR=/usr/lib/kodi \
        -DCMAKE_BUILD_TYPE=Release \
	    -DADDONS_TO_BUILD=$_gitnameff \
	    -DADDON_SRC_PREFIX="../$_gitnameff/.." \
	    "../$_gitname/cmake/addons"
  FFMPEG_PATH=$srcdir/kodi-build/build make -j$(nproc) 
}

# kodi
# components: kodi
package_kodi-nexus-mpp-git() {
  pkgdesc="A software media player and entertainment hub for digital media (Nexus branch) with Rockchip MPP hardware acceleration"
  depends=(
    'bluez-libs' 'curl' 'dav1d' 'desktop-file-utils' 'hicolor-icon-theme'
    'lcms2' 'libass' 'libbluray' 'libcdio' 'libcec' 'libmicrohttpd' 'libnfs'
    'libplist' 'libpulse' 'libva' 'libvdpau' 'libxslt' 'lirc' 'mariadb-libs'
    'mesa' 'python-pillow' 'python-pycryptodomex' 'python-simplejson'
    'shairplay' 'smbclient' 'sqlite' 'taglib' 'tinyxml'
    'libxrandr' 'libxkbcommon' 'waylandpp' 'libinput'
    'pcre' 'flatbuffers' 'mpp-git' 'librga-multi'
  )
  [[ -n "$_clangbuild" ]] && depends+=('glu')

  optdepends=(
    'afpfs-ng: Apple shares support'
    'bluez: Blutooth support'
    'python-pybluez: Bluetooth support'
    'pulseaudio: PulseAudio support'
    'upower: Display battery level'
  )
  provides=("kodi=${pkgver}" 'kodi-x11' 'kodi-wayland' 'kodi-gbm')
  conflicts=('kodi' 'kodi-x11' 'kodi-wayland' 'kodi-gbm')

  _components=(
    'kodi'
    'kodi-bin'
  )

  cd kodi-build
  for _cmp in ${_components[@]}; do
  DESTDIR="$pkgdir" /usr/bin/cmake \
    -DCMAKE_INSTALL_COMPONENT="$_cmp" \
     -P cmake_install.cmake
  done
  
  # avoid error <general>: GetDirectory - Error getting /usr/lib/kodi/addons
  mkdir -p "$pkgdir"/usr/lib/kodi/addons
}

# kodi-eventclients
# components: kodi-eventclients-common kodi-eventclients-ps3 kodi-eventclients-kodi-send
package_kodi-nexus-mpp-git-eventclients() {
  pkgdesc="Kodi Event Clients (Nexus branch)"
  provides=("kodi-eventclients=${pkgver}")
  conflicts=('kodi-eventclients')
  optdepends=(
    'kodi: local machine eventclient use'
    'python: most eventclients are implemented in python'
  )

  _components=(
    'kodi-eventclients-common'
    'kodi-eventclients-ps3'
    'kodi-eventclients-kodi-send'
  )

  cd kodi-build
  for _cmp in ${_components[@]}; do
    DESTDIR="$pkgdir" /usr/bin/cmake \
      -DCMAKE_INSTALL_COMPONENT="$_cmp" \
      -P cmake_install.cmake
  done
}

# kodi-tools-texturepacker
# components: kodi-tools-texturepacker
package_kodi-nexus-mpp-git-tools-texturepacker() {
  pkgdesc="Kodi Texturepacker tool (Nexus branch)"
  provides=("kodi-tools-texturepacker=${pkgver}")
  conflicts=('kodi-tools-texturepacker')
  depends=('libpng' 'giflib' 'libjpeg-turbo' 'lzo')

  _components=(
    'kodi-tools-texturepacker'
  )

  cd kodi-build
  for _cmp in ${_components[@]}; do
    DESTDIR="$pkgdir" /usr/bin/cmake \
      -DCMAKE_INSTALL_COMPONENT="$_cmp" \
      -P cmake_install.cmake
  done
}

package_kodi-nexus-mpp-git-ffmpegdirect() {
  pkgdesc="Inputstream ffmpegdirect kodi binary addon (Nexus branch) supporting Rockchip MPP hardware acceleration"
  provides=('kodi-addon-inputstream-ffmpegdirect')
  conflicts=('kodi-addon-inputstream-ffmpegdirect')
  depends=('kodi' 'kodi-nexus-mpp-git')
  
  cd "$srcdir/ffdirect-build"
  install -d "${pkgdir}/usr"
  mv .install/lib "${pkgdir}/usr/"
  mv .install/share "${pkgdir}/usr/"
}

# kodi-dev
# components: kodi-addon-dev kodi-eventclients-dev
package_kodi-nexus-mpp-git-dev() {
  pkgdesc="Kodi dev files (Nexus branch) with Rockchip MPP hardware acceleration"
  depends=('kodi-nexus-mpp-git')
  provides=("kodi-nexus-dev=${pkgver}" "kodi-dev=${pkgver}")
  conflicts=('kodi-nexus-dev' "kodi-dev")

  _components=(
    'kodi-addon-dev'
    'kodi-eventclients-dev'
  )

  cd kodi-build
  for _cmp in ${_components[@]}; do
    DESTDIR="$pkgdir" /usr/bin/cmake \
      -DCMAKE_INSTALL_COMPONENT="$_cmp" \
      -P cmake_install.cmake
  done
}