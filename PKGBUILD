# Maintainer: Jonathan Ball <92324185+ball2jh@users.noreply.github.com>
pkgname=claude-kitty-hypr
pkgver=1.0.0
pkgrel=1
pkgdesc="Visual feedback for Claude Code via Kitty tabs and Hyprland borders"
arch=('any')
url="https://github.com/ball2jh/claude-kitty-hypr"
license=('MIT')
depends=('jq')
optdepends=(
    'kitty: terminal tab color and title integration'
    'hyprland: window border color integration'
)
install=claude-kitty-hypr.install
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('SKIP')

package() {
    cd "$pkgname-$pkgver"
    install -Dm755 claude-kitty-hypr "$pkgdir/usr/bin/claude-kitty-hypr"
    install -Dm644 config.example "$pkgdir/usr/share/$pkgname/config.example"
    install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
