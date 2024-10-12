FROM esurdam/ffmpeg:latest
LABEL maintainer "Evan Surdam <esurdam@gmail.com>"

# yt-dlp version from https://github.com/yt-dlp/yt-dlp/releases
ENV YT_DLP_VERSION="2024.10.07"

RUN wget https://github.com/yt-dlp/yt-dlp/releases/download/${YT_DLP_VERSION}/yt-dlp -O /usr/local/bin/yt-dlp && \
    chmod a+rx /usr/local/bin/yt-dlp

ENTRYPOINT ["yt-dlp"]
CMD [ "--help" ]
WORKDIR     /tmp/