FROM alpine:3.16.0

ENV SOFTWARE_VERSION="4.3.1"
ENV SOFTWARE_VERSION_URL="http://ffmpeg.org/releases/ffmpeg-${SOFTWARE_VERSION}.tar.bz2"
ENV BIN="/usr/bin"

RUN cd && \
  apk update && \
  apk upgrade && \
  apk add \
  freetype-dev \
  gnutls-dev \
  lame-dev \
  libass-dev \
  libogg-dev \
  libtheora-dev \
  libvorbis-dev \
  libvpx-dev \
  libwebp-dev \
  libssh2 \
  opus-dev \
  rtmpdump-dev \
  x264-dev \
  x265-dev \
  yasm-dev && \
  apk add --no-cache --virtual \
  .build-dependencies \
  build-base \
  bzip2 \
  coreutils \
  gnutls \
  nasm \
  tar \
  x264 && \
  DIR=$(mktemp -d) && \
  cd "${DIR}" && \
  wget "${SOFTWARE_VERSION_URL}" && \
  tar xjvf "ffmpeg-${SOFTWARE_VERSION}.tar.bz2" && \
  cd ffmpeg* && \
  PATH="$BIN:$PATH" && \
  ./configure --help && \
  ./configure --bindir="$BIN" --disable-debug \
  --disable-doc \
  --disable-ffplay \
  --enable-avresample \
  --enable-gnutls \
  --enable-gpl \
  --enable-libass \
  --enable-libfreetype \
  --enable-libmp3lame \
  --enable-libopus \
  --enable-librtmp \
  --enable-libtheora \
  --enable-libvorbis \
  --enable-libvpx \
  --enable-libwebp \
  --enable-libx264 \
  --enable-libx265 \
  --enable-nonfree \
  --enable-postproc \
  --enable-small \
  --enable-version3 && \
  make -j4 && \
  make install && \
  make distclean && \
  rm -rf "${DIR}"

RUN apk del --purge .build-dependencies git && \
  rm -rf /var/cache/apk/*

ENTRYPOINT ["ffmpeg"]
CMD ["--help"]
WORKDIR     /tmp/