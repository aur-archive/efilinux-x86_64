# Contributor : Keshav P R <(the.ridikulus.rat) (aatt) (gemmaeiil) (ddoott) (ccoomm)>

_GNU_EFI_LIB_DIR="/usr/lib"

_actualname="efilinux"
pkgname="${_actualname}-x86_64"

pkgver="1.0"
pkgrel="1"
pkgdesc="Reference Implementation of a Linux Bootloader for x86_64 UEFI Firmwares"
arch=('any')
url="https://github.com/mfleming/efilinux"
license=('GPL')

makedepends=('gnu-efi')
depends=('dosfstools' 'efibootmgr')
provides=("${_actualname}" "${_pkgname}")
conflicts=("${_actualname}" "${_pkgname}")

options=('!strip' 'purge' '!libtool' 'emptydirs')
install="${_actualname}.install"

source=("efilinux-${pkgver}.tar.gz::https://github.com/mfleming/efilinux/tarball/efilinux-${pkgver}")
sha256sums=('bb7ee80d66d67937a56d0e8f2cde5e4d52f73e084b2277e6a4052bec5fc1edf2')

build() {
	
	if [[ "${CARCH}" != "x86_64" ]]; then
		echo "${pkgname} package can be built only in a x86_64 system. Exiting."
		exit 1
	fi
	
	cd "${srcdir}/mfleming-efilinux"-*
	
	## Change LIBDIR from /usr/lib64/ to /usr/lib/ in Makefile
	sed 's|/usr/lib64|/usr/lib|g' -i Makefile
	
	make clean || true
	echo
	
	CFLAGS="" ARCH="x86_64" CRT0="${_GNU_EFI_LIB_DIR}/crt0-efi-x86_64.o" LDSCRIPT="${_GNU_EFI_LIB_DIR}/elf_x86_64_efi.lds" make
	echo
	
}

package() {
	
	cd "${srcdir}/mfleming-efilinux"-*
	
	install -D -m0644 efilinux.efi "${pkgdir}/boot/efi/EFI/arch/efilinux/efilinuxx64.efi"
	
	rm -rf "${srcdir}/mfleming-efilinux"-*
	
}
