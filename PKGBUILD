pkgname=libspice
pkgver=0.15.2
protocol_ver=0.14.3
pkgrel=1
pkgdesc='Simple Protocol for Independent Computing Environments'
arch=('x86_64')
url='https://www.spice-space.org'
license=('LGPL-2.1-or-later')
depends=('pixman' 'openssl' 'libjpeg-turbo' 'zlib')
makedepends=()
source=("https://www.spice-space.org/download/releases/spice-server/spice-${pkgver}.tar.bz2" "https://www.spice-space.org/download/releases/spice-protocol-${protocol_ver}.tar.xz")
sha512sums=('c8f273b9e97ef38a03b331f7d32c5f0a09d540523fe626568c845152cbd22273a92b3a08bc13fa2e061b913ad16ceb7cbddf142655cd9cdcd8eb5f646fa6aa26' '9e35fd0d9be14074a482bdb20fe6954e5f0a616d0ad60da63a065435df2b169ec134a95d5756df73e2606c7497c9bf0427023d4e5ebfbb1abb181cf8020879a6')
src_name="spice-${pkgver}"
protocol_src_name="spice-protocol-${protocol_ver}"

build() {
    protocol_src_name_abs="$(realpath ${protocol_src_name})"
    
    # Install spice-protocol for internal use
    cd "${protocol_src_name}"
    mkdir protocol-inst
    meson setup build --prefix="${protocol_src_name_abs}/protocol-inst"
    cd build
    meson install
    cd ../..

    # Now prepare it for the system installation
    cd "${protocol_src_name}"
    rm -rf build
    meson setup build --prefix="/usr"
    cd ..

    # SPICE build
    cd "${src_name}"
    mkdir build
    cd build
    PKG_CONFIG_PATH="${protocol_src_name_abs}/protocol-inst/share/pkgconfig" ../configure --prefix=/usr
    make -j$(nproc)
}

package() {
    # Install the protocols first
    cd "${protocol_src_name}/build"
    DESTDIR=${pkgdir} meson install
    cd ../..

    # And now SPICE
    cd "${src_name}/build"
    DESTDIR=${pkgdir} make install
}
