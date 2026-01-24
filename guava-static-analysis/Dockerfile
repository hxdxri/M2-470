FROM ubuntu:24.04

ARG DEBIAN_FRONTEND=noninteractive

# Versions pinned for reproducibility
ARG CHECKSTYLE_VERSION=10.12.4
ARG CK_VERSION=0.7.1
ARG SEMGREP_VERSION=1.94.0

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        openjdk-17-jdk-headless \
        python3 \
        python3-pip \
        curl \
        ca-certificates \
        git \
        unzip \
    && rm -rf /var/lib/apt/lists/*

# Install Checkstyle
RUN curl -fsSL -o /opt/checkstyle.jar \
      https://github.com/checkstyle/checkstyle/releases/download/checkstyle-${CHECKSTYLE_VERSION}/checkstyle-${CHECKSTYLE_VERSION}-all.jar

# Install CK (Chidamber & Kemerer metrics tool)
RUN curl -fsSL -o /opt/ck.jar \
      https://github.com/mauricioaniche/ck/releases/download/${CK_VERSION}/ck-${CK_VERSION}-with-dependencies.jar

# Install Semgrep
RUN python3 -m pip install --no-cache-dir semgrep==${SEMGREP_VERSION}

ENV JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
ENV PATH="$JAVA_HOME/bin:$PATH"

WORKDIR /workspace

# Create expected directories
RUN mkdir -p /workspace/guava /workspace/config /workspace/scripts /workspace/results /workspace/logs

CMD ["bash"]
