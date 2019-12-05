pkgname=libwnck3
pkgver=3.32.0+10+g74e0c20
pkgrel=1
pkgdesc="Library to manage X windows and workspaces (via pagers, tasklists, etc.)"
url="https://gitlab.gnome.org/GNOME/libwnck"
arch=(x86_64)
license=(LGPL)
depends=(gtk3 startup-notification)
makedepends=(gobject-introspection git meson)
optdepends=(gtk-doc)
_commit=74e0c20bcc9aba38636364d162e9b7daa225a003  # a few commits after tag 3.32.0, needed for notification and memory leak fixes
source=("git+https://gitlab.gnome.org/GNOME/libwnck.git#commit=$_commit")
sha256sums=('SKIP')

pkgver() {
    cd libwnck
    git describe --tags | sed 's/-/+/g'
}

build() {
    meson libwnck build -D gtk_doc=false # Currently not possible to compile with docs: https://gitlab.gnome.org/GNOME/libwnck/issues/140
    ninja -C build
}

check() {
    meson test -C build --print-errorlogs
}

package() {
    DESTDIR="$pkgdir" meson install -C build
}
