#!/usr/bin/env bash
# shellcheck disable=2034,2148,2154
# Maintainer: SkyyySi
# Contributor: Chocobo1 <chocobo1 AT archlinux DOT net>
# Contributor: Lukas Fleischer <lfleischer@archlinux.org>
# Contributor: Daurnimator <daurnimator@archlinux.org>
# Contributor: Caleb Maclennan <caleb@alerque.com>
# Contributor: Bartłomiej Piotrowski <bpiotrowski@archlinux.org>
# Contributor: Chris Brannon <chris@the-brannons.com>
# Contributor: Paulo Matias <matiasΘarchlinux-br·org>
# Contributor: Anders Bergh <anders1@gmail.com>

pkgbase='luajit'
pkgname="${pkgbase}-lua52-git"
_ct='1744978152'
pkgver=2.1.1744318430
pkgrel=1
pkgdesc='Just-In-Time (JIT) compiler for the Lua programming language, with extended Lua 5.2 compatibility enabled'
arch=( 'x86_64' 'i686' 'pentium4' 'armv7h' 'aarch64' )
url='https://luajit.org/'
license=( 'MIT' )
depends=( 'gcc-libs' )
makedepends=( 'git' )
provides=( "${pkgbase}" "${pkgbase}-git" )
conflicts=( "${pkgbase}" "${pkgbase}-git" )
source=( "git+${url}git/${pkgbase}.git" )
sha256sums=( 'SKIP' )

pkgver() {
	cd "${pkgbase}" || exit 1

	_ct=$(git show --no-patch --format='%ct')

	# v2.1
	_tag=$(
		git tag --list --sort -v:'refname' |
		grep --extended-regexp -- '^v?[0-9\.]+ROLLING$' |
		head --lines 1 |
		sed -- 's/^v//;s/\.ROLLING$//'
	)

	printf '%s.%s' "${_tag}" "${_ct}"
}

build() {
	cd "${pkgbase}" || exit 1

	make XCFLAGS=' -DLUAJIT_ENABLE_LUA52COMPAT' BUILDMODE='dynamic' TARGET_STRIP=' @:' amalg
}

package() {
	cd "${pkgbase}" || exit 1

	make DESTDIR="${pkgdir}" PREFIX='/usr' install
	install -Dm644 'COPYRIGHT' -t "${pkgdir}/usr/share/licenses/${pkgbase}"
}
