# Maintainer: Jim Pryor <profjim@jimpryor.net>
# Warning: The chicken-* egg PKGBUILDS in AUR are auto-generated.
#          Please report errors you notice so that I can tweak the generation script.

pkgname=chicken-test
pkgver=0.9.8
pkgrel=4
pkgdesc="Chicken Scheme Egg: Yet Another Testing Utility"
arch=('i686' 'x86_64')
url="http://chicken.wiki.br/eggref/4/test"
license=('BSD')
depends=('chicken>=4.5.0'  )
options=(docs !libtool !emptydirs)
install="chicken.install"
source=("$pkgname-$pkgver.chunked::http://chicken.kitten-technologies.co.uk/henrietta.cgi?name=test&version=$pkgver"
		"$pkgname-$pkgver.html::http://chicken.wiki.br/eggref/4/test.html")
md5sums=('7007a6359cc78f760e535073377ccb91' '465bb674322155590bed021130ce629f')

build() {
	# unchunk the blob that was downloaded from henrietta
	cd "$srcdir"
	mkdir -p "test-$pkgver"
	cat "$pkgname-$pkgver.chunked" | while :; do
		while read -r bar ver endbar fname len; do
			[[ -n "$ver" ]] && break
		done
		[[ "$endbar" = "|#" ]] || fname="$ver" len="$endbar"
		[[ -z "$fname" ]] && break
		fname="${fname:1:${#fname}-2}" # delete quotes around fname
		if [[ "${fname: -1}" == / ]]; then
			mkdir -p "test-$pkgver/$fname"
		elif [[ "$len" -eq 0 ]]; then
			touch "test-$pkgver/$fname"
		else
			dd iflag=fullblock of="test-$pkgver/$fname" ibs="$len" count=1 2>/dev/null
		fi
	done
	

	cd "$srcdir/test-$pkgver"
	cp ../$pkgname-$pkgver.html test.html
	
	
	mkdir -p "$pkgdir/usr/lib/chicken/5" "$pkgdir/usr/share/chicken/test"
		
	chicken-install -p "$pkgdir/usr"
	
		install -Dm644 "test.html" "$pkgdir/usr/share/doc/$pkgname/test.html"
}
