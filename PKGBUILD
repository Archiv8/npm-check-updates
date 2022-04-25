#!/bin/bash

# Disable various shellcheck rules that produce false positives in this file.
# Repository rules should be added to the .shellcheckrc file located in the
# repository root directory, see https://github.com/koalaman/shellcheck/wiki
# and https://archiv8.github.io for further information.
# shellcheck disable=SC2034,SC2154
# ToDo: Add files: User documentation
# ToDo: Add files: Tooling
# FixMe: Namcap warnings and errors

# Maintainer: Ross Clark <archiv8@artisteducator.com>
# Contributor: Ross Clark <archiv8@artisteducator.com>

pkgname=npm-check-updates
pkgdesc='Find newer versions of dependencies than what your package.json or bower.json allows'
pkgver=12.0.5
pkgrel=1
arch=('any')
url='https://github.com/tjunnone/npm-check-updates'
license=('Apache')
depends=('nodejs-nopt' 'npm' 'semver')
source=(https://registry.npmjs.org/$pkgname/-/$pkgname-$pkgver.tgz)
noextract=($pkgname-$pkgver.tgz)
sha512sums=('9ecd658810688308e6395658fcf620788a1aac8b7074e481c5c7090d928a931b0c91781eb3f069e42027408bd8c25b33e9f07240916fa9748eab0214058ea0a5')

package() {
  npm install -g --prefix "$pkgdir"/usr "$srcdir"/$pkgname-$pkgver.tgz

  # Experimental dedup
  rm -r "$pkgdir"/usr/lib/node_modules/$pkgname/node_modules/{,.bin/}nopt
  rm -r "$pkgdir"/usr/lib/node_modules/$pkgname/node_modules/{,.bin/}semver

  # Non-deterministic race in npm gives 777 permissions to random directories.
  # See https://github.com/npm/npm/issues/9359 for details.
  chmod -R u=rwX,go=rX "$pkgdir"

  # npm installs package.json owned by build user
  # https://bugs.archlinux.org/task/63396
  chown -R root:root "$pkgdir"
}
