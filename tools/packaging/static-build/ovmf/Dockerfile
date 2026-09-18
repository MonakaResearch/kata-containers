# Copyright (c) 2022 IBM
#
# SPDX-License-Identifier: Apache-2.0

FROM ubuntu:22.04
ENV DEBIAN_FRONTEND=noninteractive
ENV CURL_CA_BUNDLE=/etc/ssl/certs/ca-certificates.crt
ENV GIT_SSL_CAINFO=/etc/ssl/certs/ca-certificates.crt

COPY proxy.crt /tmp/proxy.crt

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        ca-certificates \
        curl \
        g++ \
        gcc \
        git \
        iasl  \
        make \
        nasm \
        python-is-python3 \
        python3 \
        python3-distutils \
        uuid-dev && \
    if [ -s /tmp/proxy.crt ]; then \
        cp /tmp/proxy.crt /usr/local/share/ca-certificates/proxy.crt && \
        update-ca-certificates; \
    fi && \
    apt-get clean && rm -rf /var/lib/lists/
