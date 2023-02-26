# Reference: <https://postmarketos.org/devicepkg>
pkgname=device-thwc-ufi001c
pkgdesc="Tong Heng Wei Chuang ufi-001c/ufi-001b 4G Modem Stick"
pkgver=0.1
pkgrel=0
url="https://postmarketos.org"
license="MIT"
arch="aarch64"
options="!check !archcheck"
depends="postmarketos-base mkbootimg linux-postmarketos-qcom-msm8916
	 soc-qcom-msm8916 soc-qcom-msm8916-rproc
"
makedepends="devicepkg-dev"
source="deviceinfo"
subpackages="$pkgname-nonfree-firmware:nonfree_firmware"
_pmb_select="soc-qcom-msm8916-rproc"

build() {
	devicepkg_build $startdir $pkgname
}

package() {
	devicepkg_package $startdir $pkgname
}

nonfree_firmware() {
	pkgdesc="GPU/WiFi/BT/Modem/Video firmware"
	depends="firmware-qcom-adreno-a300 msm-firmware-loader
		 firmware-qcom-msm8916-wcnss firmware-huawei-y635-wcnss-nv
		 firmware-qcom-msm8916-venus"
	mkdir "$subpkgdir"
}

sha512sums="
b8c1f6268c3336c4c0ea466cb2fc1d640e2b5d723854003cd7454be52f2a2334d1452164b997fe4eaad8a34b4eefd6b4f39a49075a5b58edf31d88ecc871dec5  deviceinfo
"
