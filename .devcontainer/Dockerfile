FROM mcr.microsoft.com/devcontainers/base:ubuntu-22.04

# 1. Install system dependencies
RUN apt-get update && apt-get install -y \
    perl \
    wget \
    xz-utils \
    libfontconfig1 \
    && rm -rf /var/lib/apt/lists/*

# 2. Use a specific TeX Live installer that is faster
RUN wget -qO- https://github.com/reuterbal/texlive-tiny/releases/latest/download/install-tl-unx.tar.gz | tar -xz -C /tmp && \
    mv /tmp/install-tl-* /tmp/install-tl && \
    printf "selected_scheme scheme-basic\ninstopt_adjustpath 1" > /tmp/install-tl/texlive.profile && \
    /tmp/install-tl/install-tl --profile=/tmp/install-tl/texlive.profile && \
    rm -rf /tmp/install-tl

# 3. Set the PATH (Crucial step)
ENV PATH="/usr/local/texlive/2026/bin/x86_64-linux:${PATH}"

# 4. Use the TeX Manager to install latexmk specifically
RUN tlmgr update --self && \
    tlmgr install latexmk
