
FROM mcr.microsoft.com/devcontainers/base:ubuntu-24.04

# 1. Install ESSENTIAL system dependencies for the TeX Live installer
RUN apt-get update && apt-get install -y \
    perl \
    wget \
    xz-utils \
    gnupg \
    libio-socket-ssl-perl \
    ca-certificates \
    && rm -rf /var/lib/apt/lists/*

# 2. Download and run the installer
# Adding --no-check-certificate can help if your Codespace has SSL issues
RUN wget --no-check-certificate http://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz && \
    mkdir /install-tl-unx && \
    tar -xvf install-tl-unx.tar.gz -C /install-tl-unx --strip-components=1 && \
    # Create the profile to automate the installation
    echo "selected_scheme scheme-full" > /install-tl-unx/texlive.profile && \
    echo "tlpdbopt_install_docfiles 0" >> /install-tl-unx/texlive.profile && \
    echo "tlpdbopt_install_srcfiles 0" >> /install-tl-unx/texlive.profile && \
    # Run the installation using a specific repository to avoid mirror-selection errors
    /install-tl-unx/install-tl --profile=/install-tl-unx/texlive.profile --repository http://mirror.ctan.org/systems/texlive/tlnet/ && \
    rm -rf install-tl-unx.tar.gz /install-tl-unx

# 3. Correct Path for 2026
ENV PATH="/usr/local/texlive/2026/bin/x86_64-linux:${PATH}"

# 4. Verify and install specific research packages
RUN tlmgr install multirow colortbl cite tools
