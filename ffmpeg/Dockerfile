FROM alpine:3.17
LABEL maintainer "Evan Surdam <esurdam@gmail.com>"

ENV SOFTWARE_VERSION="7.1"
ENV SOFTWARE_VERSION_URL="https://ffmpeg.org/releases/ffmpeg-${SOFTWARE_VERSION}.tar.bz2"
ENV BIN="/usr/bin"

RUN apk add --no-cache \
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
    x265-dev

RUN apk add --no-cache --virtual .build-dependencies \
    build-base \
    bzip2 \
    coreutils \
    gnutls \
    nasm \
    tar \
    x264-dev \
    yasm \
    wget

RUN wget -O ffmpeg.tar.bz2 "${SOFTWARE_VERSION_URL}" && \
    tar xjf ffmpeg.tar.bz2 && \
    cd ffmpeg-${SOFTWARE_VERSION} && \
    ./configure \
    --bindir="$BIN" \
    --disable-debug \
    --disable-doc \
    --disable-ffplay \    
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
    make -j$(nproc) && \
    make install && \
    cd .. && \
    rm -rf ffmpeg*

RUN apk del --purge .build-dependencies && \
    rm -rf /var/cache/apk/*

ENTRYPOINT ["ffmpeg"]
CMD ["--help"]
WORKDIR /tmp
