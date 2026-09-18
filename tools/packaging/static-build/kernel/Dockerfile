# Copyright (c) 2021 Intel Corporation
#
# SPDX-License-Identifier: Apache-2.0

FROM ubuntu:22.04
ENV DEBIAN_FRONTEND=noninteractive
ENV INSTALL_IN_GOPATH=false

ARG http_proxy
ARG https_proxy
ARG no_proxy
ENV http_proxy=${http_proxy} \
    https_proxy=${https_proxy} \
    no_proxy=${no_proxy} \
    CURL_CA_BUNDLE=/etc/ssl/certs/ca-certificates.crt

COPY install_yq.sh /usr/bin/install_yq.sh
COPY proxy.crt /tmp/proxy.crt

# kernel deps
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
	    bc \
	    bison \
	    build-essential \
	    ca-certificates \
	    curl \
	    debhelper \
	    dwarves \
	    flex \
	    git \
	    iptables \
	    kmod \
	    libdw-dev \
	    libelf-dev \
	    libssl-dev \
	    gettext \
	    rsync \
	    cpio \
	    patch \
	    python3 && \
    if [ -s /tmp/proxy.crt ]; then \
        cp /tmp/proxy.crt /usr/local/share/ca-certificates/proxy.crt && \
        update-ca-certificates; \
    fi && \
    apt-get clean && apt-get autoclean && rm -rf /var/lib/apt/lists/*

RUN install_yq.sh
