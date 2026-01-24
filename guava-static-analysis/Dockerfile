FROM amazoncorretto:17-alpine

ARG CHECKSTYLE_VERSION=10.12.4
ARG CK_VERSION=0.7.1
ARG SEMGREP_VERSION=1.94.0

# Install tools via apk (no apt, no Ubuntu)
RUN apk add --no-cache \
    python3 \
    py3-pip \
    curl \
    git \
    unzip \
    bash


WORKDIR /workspace
RUN mkdir -p guava config scripts results logs

CMD ["bash"]
