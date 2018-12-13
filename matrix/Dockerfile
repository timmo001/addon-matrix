ARG BUILD_FROM=hassioaddons/base:2.3.0
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# TODO
# - Add riot web frontend
# - Test connection with desktop, web and mobile clients

# Setup Matrix Synapse
RUN \
    apk add --no-cache --virtual .build-dependencies \
        build-base=0.5-r1 \
        libffi-dev=3.2.1-r4 \
        libjpeg-turbo-dev=1.5.3-r3 \
        libressl-dev=2.7.4-r0 \
        libxslt-dev=1.1.32-r0 \
        linux-headers=4.4.6-r2 \
        postgresql-dev=10.5-r0 \
        py2-pip=10.0.1-r0 \
        zlib-dev=1.2.11-r1 \
    \
    && apk add --no-cache \
        libffi=3.2.1-r4 \
        libjpeg-turbo=1.5.3-r3 \
        libpq=10.5-r0 \
        libressl=2.7.4-r0 \
        libxslt=1.1.32-r0 \
        nginx=1.14.2-r0 \
        py-setuptools=39.1.0-r0 \
        py2-lxml=4.2.2-r0 \
        py2-msgpack=0.5.6-r0 \
        py2-pillow=4.3.0-r0 \
        py2-psycopg2=2.7.5-r0 \
        py2-pynacl=1.2.1-r1	\
        py2-six=1.11.0-r0 \
        python2-dev=2.7.15-r1 \
        su-exec=0.2-r0 \
        zlib=1.2.11-r1 \
    \
    && pip2 install --upgrade pip==18.1 \
    && pip2 install \
        pysaml2==4.6.5 \
        matrix-synapse==0.33.9 \
    \
    && apk del --purge .build-dependencies \
    && mkdir -p /opt/riot-im \
    && wget -O riot.tar.gz https://github.com/vector-im/riot-web/releases/download/v0.17.8/riot-v0.17.8.tar.gz \
    && tar xzf riot.tar.gz -C /opt/riot-im --strip 1 \
    && rm riot.tar.gz

# Copy root filesystem
COPY rootfs /

# Build arugments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_REF
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="Matrix" \
    io.hass.description="A secure and decentralized communication platform." \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Franck Nijhof <frenck@addons.community>" \
    org.label-schema.description="A secure and decentralized communication platform." \
    org.label-schema.build-date=${BUILD_DATE} \
    org.label-schema.name="Matrix" \
    org.label-schema.schema-version="1.0" \
    org.label-schema.url="https://community.home-assistant.io" \
    org.label-schema.usage="https://github.com/hassio-addons/addon-matrix/tree/master/README.md" \
    org.label-schema.vcs-ref=${BUILD_REF} \
    org.label-schema.vcs-url="https://github.com/hassio-addons/addon-matrix" \
    org.label-schema.vendor="Community Hass.io Add-ons"