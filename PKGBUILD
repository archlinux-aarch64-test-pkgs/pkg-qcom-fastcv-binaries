# Maintainer: Xilin Wu <sophon@radxa.com>
# Upstream: Qualcomm FastCV prebuilt binaries

pkgname=qcom-fastcv-binaries
pkgver=1.8.9
pkgrel=1
pkgdesc="Qualcomm FastCV computer vision library (prebuilt binary)"
arch=('aarch64')
url="https://softwarecenter.qualcomm.com"
license=('LicenseRef-Qualcomm-EULA')
depends=('qcom-fastrpc' 'glib2')
options=('!strip')

_datestamp=260805

source=("https://qartifactory-edge.qualcomm.com/artifactory/qsc_releases/software/chip/component/computervision-fastcv.qclinux.0.1/${_datestamp}/prebuilt_yocto_master/${pkgname}_${pkgver}_armv8a.tar.gz")
sha256sums=('06bbb3283f9a018b41d9ec79b347587453f24f7bc76b469f89a09142579e3b2e')

package() {
  cd "$srcdir"

  # Shared libraries
  install -Dm755 usr/lib/libfastcvopt.so.1.8.0      "$pkgdir/usr/lib/libfastcvopt.so.1.8.0"
  install -Dm755 usr/lib/libfastcvdsp_stub.so.1.8.0  "$pkgdir/usr/lib/libfastcvdsp_stub.so.1.8.0"

  cd "$pkgdir/usr/lib"
  ln -s libfastcvopt.so.1.8.0     libfastcvopt.so.1
  ln -s libfastcvopt.so.1.8.0     libfastcvopt.so
  ln -s libfastcvdsp_stub.so.1.8.0 libfastcvdsp_stub.so.1
  ln -s libfastcvdsp_stub.so.1.8.0 libfastcvdsp_stub.so
  cd "$srcdir"

  # DSP libraries
  local _dsp_base="usr/lib/dsp/cdsp/cv"
  for _dir in "$_dsp_base"/v*/*/; do
    for _so in "$_dir"*.so; do
      [ -f "$_so" ] || continue
      install -Dm755 "$_so" "$pkgdir/$_so"
    done
  done

  # Headers
  install -Dm644 usr/include/fastcv/fastcv.h    "$pkgdir/usr/include/fastcv/fastcv.h"
  install -Dm644 usr/include/fastcv/fastcvDsp.h  "$pkgdir/usr/include/fastcv/fastcvDsp.h"
  install -Dm644 usr/include/fastcv/fastcvExt.h  "$pkgdir/usr/include/fastcv/fastcvExt.h"

  # Pkgconfig
  install -Dm644 usr/lib/pkgconfig/qcom-fastcv-binaries.pc \
    "$pkgdir/usr/lib/pkgconfig/qcom-fastcv-binaries.pc"

  # Test binary
  install -Dm755 usr/bin/fastcv_simple_test64 "$pkgdir/usr/bin/fastcv_simple_test64"

  # License / documentation
  install -Dm644 usr/share/doc/qcom-fastcv-binaries/NOTICE \
    "$pkgdir/usr/share/licenses/$pkgname/NOTICE"
  install -Dm644 usr/share/doc/qcom-fastcv-binaries/NOLOGINBINARYLICENSEQTI.pdf \
    "$pkgdir/usr/share/licenses/$pkgname/NOLOGINBINARYLICENSEQTI.pdf"
}
