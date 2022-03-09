# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.224.2/containers/rust/.devcontainer/base.Dockerfile

# [Choice] Debian OS version (use bullseye on local arm64/Apple Silicon): buster, bullseye
ARG VARIANT="bullseye"
FROM mcr.microsoft.com/vscode/devcontainers/rust:0-${VARIANT}

# [Optional] Uncomment this section to install additional packages.
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
        gdb-multiarch \
        automake \
        autoconf \
        build-essential \
        texinfo \
        libtool \
        libftdi-dev \
        libusb-1.0-0-dev \
        pkg-config

# Install Rust Cortex-M target
RUN rustup target install thumbv6m-none-eabi

# Install OpenOCD
RUN git clone https://github.com/raspberrypi/openocd.git --branch picoprobe --depth=1 \
    && cd openocd \
    && ./bootstrap \
    && ./configure --disable-werror --enable-ftdi --enable-sysfsgpio --enable-bcm2835gpio --enable-picoprobe \
    && make -j4 \
    && make install
