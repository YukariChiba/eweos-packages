# Maintainer: Aleksana QwQ <me@aleksana.moe>
# Contributor sheepla <hk7g9x43 at anonaddy.me>

pkgname=fzpac
pkgver=2.0.5
pkgrel=1
pkgdesc="Arch Linux TUI package finder with fzf"
arch=("any")
url="https://github.com/sheepla/fzpac"
license=("MIT")
depends=("fzf")
optdepends=(
    "skim: for another fuzzy finder support"
    "bash-completion: for bash completion support"
    "zsh-completions: for zsh completion support"
    "fish: for fish completion support"
)
source=("${pkgname}-${pkgver}.tar.gz::${url}/archive/refs/tags/v${pkgver}.tar.gz")
sha256sums=('ef2f8cac36ac8270b5f08169865d3998f8cb68ebf5e252623e5be36ad0c92cfe')

package() {
    cd "${srcdir}/${pkgname}-${pkgver}"
    PREFIX="${pkgdir}/usr" make install
}

