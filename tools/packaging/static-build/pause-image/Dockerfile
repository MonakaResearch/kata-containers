# Copyright (c) 2024 Intel
#
# SPDX-License-Identifier: Apache-2.0
FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

ARG http_proxy
ARG https_proxy
ARG no_proxy
ENV http_proxy=${http_proxy} \
    https_proxy=${https_proxy} \
    no_proxy=${no_proxy} \
    CURL_CA_BUNDLE=/etc/ssl/certs/ca-certificates.crt

COPY proxy.crt /tmp/proxy.crt

SHELL ["/bin/bash", "-o", "pipefail", "-c"]
RUN apt-get update && \
    apt-get --no-install-recommends -y install \
    ca-certificates \
    curl \
    umoci \
    skopeo && \
    if [ -s /tmp/proxy.crt ]; then \
        cp /tmp/proxy.crt /usr/local/share/ca-certificates/proxy.crt && \
        update-ca-certificates; \
    fi
