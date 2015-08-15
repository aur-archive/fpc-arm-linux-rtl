pkgname=fpc-arm-linux-rtl
pkgver=2.6.2
pkgrel=2
pkgdesc="Free Pascal runtime library for ARM Linux."
arch=('any')
url="http://www.freepascal.org/"
license=('GPL' 'LGPL' 'custom')
depends=('fpc=2.6.2' 'ppcrossarm' 'arm-linux-binutils')
makedepends=(ppcrossarm arm-linux-binutils)
source=("ftp://ftp.freepascal.org/pub/fpc/dist/$pkgver/source/fpcbuild-$pkgver.tar.gz"
	"ftp://ftp.freepascal.org/pub/fpc/dist/$pkgver/source/patches.tar.gz")
md5sums=('89c7e60db6280f3d5cc006a4a9ff43a9'
	 'bb4deac73218d7d179cefe2d8ccf3699')

build() {
  cd "${srcdir}/fpcbuild-$pkgver"
	  patch -p0 -i ../patches/fpc-2.6.2_001.patch || return 1
	  patch -p0 -i ../patches/fpc-2.6.2_002.patch || return 1
	  patch -p0 -i ../patches/fpc-2.6.2_003.patch || return 1
  cd "${srcdir}/fpcbuild-$pkgver/fpcsrc"
	  patch -p0 -i ../../patches/fpc-2.6.2_004.patch || return 1


  cd "${srcdir}/fpcbuild-$pkgver/fpcsrc/compiler"
  fpcmake -Tall
  cd ../..
  make NOGDB=1 build OS_TARGET=linux CPU_TARGET=arm NODOC=1
}

package() {
  cd "${srcdir}/fpcbuild-$pkgver"
  make NOGDB=1 PREFIX="${pkgdir}/usr" crossinstall OS_TARGET=linux CPU_TARGET=arm NODOC=1
  rm -rf "${pkgdir}/usr/bin"
  rm "$pkgdir/usr/lib/fpc/$pkgver/ppcrossarm"

  cat << 'EOM'
  ==> PLEASE NOTE:
  ==> Please be sure to copy fpcbuild-x.x.x.tar.gz to the extracted package folders
  ==> of any RTLs or other FPC cross compilers you intend to build, as Free Pascal's
  ==> FTP server is very low bandwidth. Thanks!
EOM
}

