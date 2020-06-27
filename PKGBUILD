# Maintainer: redfish <redfish@galactica.pw>

pkgname=python-ipfshttpclient

# Released on github and PyPI
#   Status: broken with 0.6.0 (one test fails due to method in API request not being POST)
#_name=ipfshttpclient
#pkgver=0.4.13.2
#_relver=0.4.13 # upstream tarball name mismatches the release version

# released only on PyPi as a different package
# Status: all tests pass after the patch referenced in below
_name=ipfshttpclient4ipwb
pkgver=0.6.0

pkgrel=1
pkgdesc="Python IPFS HTTP client library"
arch=('any')
conflicts=("python-ipfsapi") # legacy name
url="https://pypi.python.org/pypi/ipfshttpclient"
license=('MIT')
depends=('python'
         'python-multiaddr'
         'python-netaddr'
         'python-requests'
         'python-setuptools'
         'python-six'
        )
checkdepends=('python-pytest' 'python-pytest-cov' 'python-pytest-ordering' 'python-pytest-mock'
	      'python-pytest-localserver' 'python-pluggy' 'python-py'
	      #python-py-cid # appears to be optional
	     )
optdepends=('go-ipfs: IPFS daemon') # an IPFS deamon is a checkdepend, but not required to be go-ipfs
#source=("https://github.com/ipfs-shipyard/py-ipfs-http-client/releases/download/${_relver}/${_name}-${pkgver}.tar.gz")
source=("https://pypi.io/packages/source/${_name::1}/${_name}/${_name}-${pkgver}.tar.gz"
	https://gist.githubusercontent.com/radfish/8bf3f64bc47c8ec123c469421ab293de/raw/d89ed69e3561961d92b1f48bad843649222f69b2/ipfshttpclient4ipwb-0.6.0-tests.patch
	https://gist.githubusercontent.com/radfish/8bf3f64bc47c8ec123c469421ab293de/raw/d89ed69e3561961d92b1f48bad843649222f69b2/ipfshttpclient4ipwb-0.6.0-rename.patch)

prepare() {
	cd "$_name-$pkgver"
	patch -p1 < ${srcdir}/ipfshttpclient4ipwb-0.6.0-tests.patch
	patch -p1 < ${srcdir}/ipfshttpclient4ipwb-0.6.0-rename.patch
	mv ipfshttpclient{4ipwb,}
}

build() {
    cd "$_name-$pkgver"
    python setup.py build
}

check() {
    cd "$_name-$pkgver"

    # To exclude tests pass: -k 'not test_name', to not eat stdout: --capture=no
    ./test/run-tests.py
}

package() {
    cd "$_name-$pkgver"
    python setup.py install --root="$pkgdir" --optimize=1 --skip-build
}

#sha256sums=('468d7c72ef309a91cf9c72a477da89f428757b32c30636da7c77a041ca01b2b3')
sha256sums=('2d0a349df35a7ae37fe1001f3b19260a65faf5fdb39cd945e71ba33a7c0dedf9'
            'af04b39810f2270e3e4449282f4ea55d8b34c3c3f4dd515674d587bd841efcce'
            '13b2d8cdce60b08d6a223455083ba674eda36c802e414daf143f416b422a797d')
