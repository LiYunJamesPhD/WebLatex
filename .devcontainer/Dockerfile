#FROM mcr.microsoft.com/devcontainers/base:ubuntu-22.04


# Change the date here to force a re-run
RUN echo "Re-running install as of 2026-03-10" 

RUN wget http://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz && \
    mkdir /tmp/install-tl && \
    tar -xzf install-tl-unx.tar.gz -C /tmp/install-tl --strip-components=1 && \
    printf "selected_scheme scheme-small\ninstopt_adjustpath 1" > /tmp/install-tl/texlive.profile && \
    ./install-tl --profile=/tmp/install-tl/texlive.profile


# 1. Install Perl and wget (required for TeX Live installer)
RUN apt-get update && apt-get install -y perl wget xz-utils libfontconfig1 && rm -rf /var/lib/apt/lists/*

# 2. Download and run the TeX Live 2026 Installer
# This uses the "scheme-small" to save time/space, but you can change it to "scheme-full"
RUN wget http://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz && \
    mkdir /tmp/install-tl && \
    tar -xzf install-tl-unx.tar.gz -C /tmp/install-tl --strip-components=1 && \
    printf "selected_scheme scheme-small\ninstopt_adjustpath 1" > /tmp/install-tl/texlive.profile && \
    /tmp/install-tl/install-tl --profile=/tmp/install-tl/texlive.profile && \
    rm -rf install-tl-unx.tar.gz /tmp/install-tl

# 3. Manually set the Path for 2026
ENV PATH="/usr/local/texlive/2026/bin/x86_64-linux:${PATH}"
