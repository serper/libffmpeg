# Contributor: Sergio Perez <sergio@pereznus.es>
# Maintainer: Sergio Perez <sergio@pereznus.es>
pkgname=ffmpeg-v4l2req
pkgver=7.1
pkgrel=0
pkgdesc="FFmpeg libraries with V4L2 Request API HW acceleration"
url="https://ffmpeg.org"
arch="all"
license="MIT"
depends="eudev"
makedepends="cmake pkgconfig git libunistring-dev gnutls-dev linux-headers eudev-dev libdrm-dev v4l-utils-dev"

subpackages="
    $pkgname-dev
    $pkgname-libs
    $pkgname-libavcodec
    $pkgname-libavformat
    $pkgname-libavutil
    $pkgname-libswresample
    $pkgname-libswscale
    $pkgname-tools
"

source="$pkgname-$pkgver.zip::https://github.com/FFmpeg/FFmpeg/archive/refs/heads/release/$pkgver.zip
FFmpeg-devel-v2-1-8-avutil-hwcontext-Add-hwdevice-type-for-V4L2-Request-API.patch
FFmpeg-devel-v2-2-8-avcodec-Add-common-V4L2-Request-API-code.patch
FFmpeg-devel-v2-3-8-avcodec-v4l2request-Probe-for-a-capable-media-and-video-device.patch
FFmpeg-devel-v2-4-8-avcodec-v4l2request-Add-common-decode-support-for-hwaccels.patch
FFmpeg-devel-v2-5-8-avcodec-Add-V4L2-Request-API-mpeg2-hwaccel.patch
FFmpeg-devel-v2-6-8-avcodec-h264dec-add-ref_pic_marking-and-pic_order_cnt-bit_size-to-slice-context.patch
FFmpeg-devel-v2-7-8-avcodec-Add-V4L2-Request-API-h264-hwaccel.patch
FFmpeg-devel-v2-8-8-avcodec-Add-V4L2-Request-API-hevc-hwaccel.patch"

prepare() {
    mv "$srcdir/FFmpeg-release-$pkgver" "$srcdir/$pkgname-$pkgver"
    default_prepare
    cd "$srcdir/$pkgname-$pkgver"
    ./configure \
        --prefix=/usr \
        --enable-shared \
        --disable-static \
        --disable-all \
        --disable-autodetect \
        --enable-swresample \
        --enable-v4l2-request \
        --enable-gnutls \
        --enable-libudev \
        --enable-libdrm \
        --enable-avcodec \
        --enable-avformat \
        --enable-decoders \
        --enable-encoders \
        --enable-demuxers \
        --enable-parsers \
        --enable-protocol='file' \
        --enable-swscale \
        --enable-zlib \
        --enable-ffmpeg \
        --enable-ffprobe \
        --enable-neon \
        --cpu=cortex-a7 \
        --extra-cflags="-mfpu=neon -mfloat-abi=hard" \
        --extra-libs="-ludev"
}

build() {
    cd "$srcdir/$pkgname-$pkgver"
    make -j$(nproc)
}

package() {
    cd "$srcdir/$pkgname-$pkgver"
    make DESTDIR="$pkgdir" install
}

dev() {
    default_dev
    replaces="ffmpeg-dev"
    conflicts="ffmpeg-dev"
}

libavcodec() {
    pkgdesc="FFmpeg libavcodec with V4L2 request support"
    provides="ffmpeg-libavcodec=$pkgver-r$pkgrel"
    replaces="ffmpeg-libavcodec"
    amove usr/lib/libavcodec.so.*
}

libavformat() {
    pkgdesc="FFmpeg libavformat with V4L2 request support"
    provides="ffmpeg-libavformat=$pkgver-r$pkgrel"
    replaces="ffmpeg-libavformat"
    amove usr/lib/libavformat.so.*
}

libavutil() {
    pkgdesc="FFmpeg libavutil with V4L2 request support"
    provides="ffmpeg-libavutil=$pkgver-r$pkgrel"
    replaces="ffmpeg-libavutil"
    amove usr/lib/libavutil.so.*
}

libswresample() {
    pkgdesc="FFmpeg libswresample with V4L2 request support"
    provides="ffmpeg-libswresample=$pkgver-r$pkgrel"
    replaces="ffmpeg-libswresample"
    amove usr/lib/libswresample.so.*
}

libswscale() {
    pkgdesc="FFmpeg libswscale with V4L2 request support"
    provides="ffmpeg-libswscale=$pkgver-r$pkgrel"
    replaces="ffmpeg-libswscale"
    amove usr/lib/libswscale.so.*
}

libs() {
    pkgdesc="Meta-package for all ffmpeg-v4l2req libraries"
    provides="ffmpeg-libs=$pkgver-r$pkgrel"
    replaces="ffmpeg-libs"
    depends="
        $pkgname-libavcodec=$pkgver-r$pkgrel
        $pkgname-libavformat=$pkgver-r$pkgrel
        $pkgname-libavutil=$pkgver-r$pkgrel
        $pkgname-libswresample=$pkgver-r$pkgrel
        $pkgname-libswscale=$pkgver-r$pkgrel
    "
    mkdir -p "$subpkgdir"
}

tools() {
    pkgdesc="FFmpeg command-line tools with V4L2 request support"
    provides="ffmpeg-tools=$pkgver-r$pkgrel"
    replaces="ffmpeg-tools"
    mkdir -p "$subpkgdir/usr/bin"
    amove usr/bin/*
}

sha512sums="
44c524f3ac808d9ce81ce4f15b9f04cc6f90cd6337757f37b7cf51a4ee8001c8ba364911e514166ba85e7d4dd78dfd4f1ff243ddd34f5c691d7f469b6e3df31f  ffmpeg-v4l2req-7.1.zip
39034dc869f68aac53e2eaf65a7b97be6ff71f88511457d34c83988a033977d94e411dae142eb27dea104a44a86827f91cf86aaf5c2987ee202eb95968006780  FFmpeg-devel-v2-1-8-avutil-hwcontext-Add-hwdevice-type-for-V4L2-Request-API.patch
9e8a0bb9d3f2bbfb2fa7840d47edc4eaa82574c5fb57784bf912ed0a34b277804bcae364014956bd778bf3ba46a626fe372a8ea548e5aef02d6b27399c7bd84e  FFmpeg-devel-v2-2-8-avcodec-Add-common-V4L2-Request-API-code.patch
d4d4a027818fdf1ad62dd9a65ade9f9b107626b4f389e1a28926251105ef26d3b45c20d0a9019d4787855c19f4241788fbb12e20e8325adef15e8b7e55499bf3  FFmpeg-devel-v2-3-8-avcodec-v4l2request-Probe-for-a-capable-media-and-video-device.patch
5469da145c62fc8db64f1b4d48dcc93fed1ad771184ba02ae8c9512de847043b5c947e15f306770aff323f98f9e7fb8f2455c9d43842afee9e4dbf73cb729a6e  FFmpeg-devel-v2-4-8-avcodec-v4l2request-Add-common-decode-support-for-hwaccels.patch
839482a02cdc5c8a8418214b8925e0c72f8ae7bf6f1050df0bd9597200d7a640857151e1b20ef1ea8f9e50f11f060a900ee94114ec3aaca26abe779aedd33b35  FFmpeg-devel-v2-5-8-avcodec-Add-V4L2-Request-API-mpeg2-hwaccel.patch
1ac06c2de7ff257b23b854810fdffa18b8138b4ffca3b64a09e4260ef3d54c9dfe4fd28ff643c9b1c876230ed39dd00b77587e114fd826bffd88d6be245000ab  FFmpeg-devel-v2-6-8-avcodec-h264dec-add-ref_pic_marking-and-pic_order_cnt-bit_size-to-slice-context.patch
2fbd5004df7b7fb643d6fdf8ce0acdc779d0132445f5b459357288e6d175d60e878f7ae417343e7748e8a86d972f9e5db109fcc034a34518af0790b7e9d2c678  FFmpeg-devel-v2-7-8-avcodec-Add-V4L2-Request-API-h264-hwaccel.patch
8e4240110824a03f26642b692d0a765571276110f4b27e81bc453424d5458a8b257db698fd28c3b07b3a228b8f6c4acd5960c892b15b427e8873cd093a825087  FFmpeg-devel-v2-8-8-avcodec-Add-V4L2-Request-API-hevc-hwaccel.patch
"
