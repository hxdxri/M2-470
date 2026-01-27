FROM amazoncorretto:17-alpine

ARG CHECKSTYLE_VERSION=10.12.4
ARG CK_VERSION=0.7.1
ARG SEMGREP_VERSION=1.149.0

# Install tools via apk (no apt, no Ubuntu)
RUN apk add --no-cache \
    python3 \
    py3-pip \
    curl \
    git \
    unzip \
    bash

# Install Semgrep via pip in a venv (PEP 668 compliant on Alpine)
# Alpine may need build deps if a musllinux wheel isn't available for the pinned version.
RUN apk add --no-cache --virtual .semgrep-build-deps \
        build-base \
        libffi-dev \
        openssl-dev \
        cargo \
    && python3 -m venv /opt/semgrep-venv \
    && /opt/semgrep-venv/bin/pip install --no-cache-dir --upgrade pip setuptools wheel \
    && /opt/semgrep-venv/bin/pip install --no-cache-dir semgrep==${SEMGREP_VERSION} \
    && ln -s /opt/semgrep-venv/bin/semgrep /usr/local/bin/semgrep \
    && apk del .semgrep-build-deps

RUN mkdir -p /opt/tools \
 && curl -L -o /opt/tools/checkstyle-${CHECKSTYLE_VERSION}-all.jar \
    https://github.com/checkstyle/checkstyle/releases/download/checkstyle-${CHECKSTYLE_VERSION}/checkstyle-${CHECKSTYLE_VERSION}-all.jar

WORKDIR /workspace
RUN mkdir -p guava config scripts results logs

CMD ["bash"]
