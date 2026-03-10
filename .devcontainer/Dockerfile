# Use a modern Ubuntu base
FROM mcr.microsoft.com/devcontainers/base:ubuntu-24.04

# Install installer dependencies
RUN apt-get update && apt-get install -y \
    perl \
    wget \
    xz-utils \
    && rm -rf /var/lib/apt/lists/*

# Download and run the TeX Live 2026 installer
RUN wget http://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz && \
    mkdir /install-tl-unx && \
    tar -xvf install-tl-unx.tar.gz -C /install-tl-unx --strip-components=1 && \
    echo "selected_scheme scheme-full" > /install-tl-unx/texlive.profile && \
    /install-tl-unx/install-tl --profile=/install-tl-unx/texlive.profile && \
    rm -r install-tl-unx.tar.gz /install-tl-unx

# Set the PATH specifically for the 2026 version
ENV PATH="/usr/local/texlive/2026/bin/x86_64-linux:${PATH}"

# Add any specific packages you need for your research
RUN tlmgr install multirow colortbl cite tools
