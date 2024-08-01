FROM alpine:3.20.2

ENV TINI_VERSION v0.19.0

RUN apk update \
        && apk upgrade \
        && apk add --no-cache bash \
        bash-doc \
        curl \
        bash-completion \
        binutils \
        zstd \
        fontconfig \
        libretls \
        musl-locales \
        musl-locales-lang \
        ttf-dejavu \
        tzdata \
        zlib \
        && rm -rf /var/cache/apk/* \
        && /bin/bash
# 设置时区为上海
RUN apk -U add tzdata && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone \
    && apk del tzdata


ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini-static /tini
RUN chmod +x /tini

ENTRYPOINT ["/tini", "--"]