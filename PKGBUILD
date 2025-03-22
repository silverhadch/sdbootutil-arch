pkgname=sdbootutil-git
pkgver="1.1"
pkgrel=1
pkgdesc="bootctl wrapper for BLS boot loaders"
arch=("any")
license=("MIT")
url="https://github.com/openSUSE/sdbootutil"
depends=(
    "dialog"
    "efibootmgr"
    "jq"
    "keyutils"
    "openssl"
    "qrencode"
    "sed"
    "udev"
    "btrfs-progs"
    "snapper"
)
makedepends=("git")
source=("git+https://github.com/silverhadch/sdbootutil-arch.git")
sha256sums=("SKIP")

build() {
    cd "$srcdir/sdbootutil"
    # No specific build process defined in the spec file
}

package() {
    cd "$srcdir/sdbootutil"

    # Install the main executable
    install -Dm755 "sdbootutil" "$pkgdir/usr/bin/sdbootutil"

    # Install Snapper plugin
    install -Dm755 "10-sdbootutil.snapper" "$pkgdir/usr/lib/snapper/plugins/10-sdbootutil.snapper"

    # Install kernel-install hook (with mkinitcpio, not dracut)
    install -Dm755 "50-sdbootutil.install" "$pkgdir/usr/lib/kernel/install.d/50-sdbootutil.install"

    # Install bash completions
    install -Dm755 "completions/bash_sdbootutil" "$pkgdir/usr/share/bash-completion/completions/sdbootutil"

    # Create necessary directories for snapper integration
    install -d -m 700 "$pkgdir/usr/share/sdbootutil"

    # Install tmpfiles configuration
    install -Dm644 "kernel-install-sdbootutil.conf" "$pkgdir/usr/lib/tmpfiles.d/kernel-install-sdbootutil.conf"


}