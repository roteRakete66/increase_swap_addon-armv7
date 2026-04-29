ARG BUILD_FROM=ghcr.io/home-assistant/amd64-base:3.22
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

ARG BASHIO_VERSION=0.16.3

# hadolint ignore=DL3018
RUN \
    apk add --no-cache \
        curl \
        jq \
    \
    && curl -J -L -o /tmp/bashio.tar.gz \
        "https://github.com/hassio-addons/bashio/archive/v${BASHIO_VERSION}.tar.gz" \
    && mkdir /tmp/bashio \
    && tar zxvf /tmp/bashio.tar.gz --strip 1 -C /tmp/bashio \
    \
    && mv /tmp/bashio/lib /usr/lib/bashio \
    && ln -sf /usr/lib/bashio/bashio /usr/bin/bashio \
    \
    && rm -rf /tmp/*

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

COPY run.sh /
RUN chmod a+x /run.sh

CMD [ "/run.sh" ]
