ARG UBUNTU_VERSION="22.04"

FROM mcr.microsoft.com/vscode/devcontainers/base:ubuntu-${UBUNTU_VERSION}

RUN export DEBIAN_FRONTEND=noninteractive \
  && set -x \
  && apt update \
  && apt install --no-install-recommends --yes \
    bc \
    build-essential \
    ca-certificates \
    clang \
    dialog \
    python3 \
    python3-dev \
    python3-distutils \
    python3-pip \
    python3-setuptools \
    python3-venv \
    srecord \
    udev \
    xz-utils \
  && apt autoremove --yes \
  && apt clean \
  && rm -rf /var/lib/apt/lists/* /var/tmp/* /tmp/*

RUN curl -sfL https://raw.githubusercontent.com/platformio/platformio-core/develop/platformio/assets/system/99-platformio-udev.rules -o /etc/udev/rules.d/99-platformio-udev.rules

RUN usermod -a -G dialout vscode \
  && usermod -a -G plugdev vscode

USER vscode

RUN curl -fsSL https://raw.githubusercontent.com/platformio/platformio-core-installer/master/get-platformio.py -o /tmp/get-platformio.py \
  && python3 /tmp/get-platformio.py \
  && mkdir -p "${HOME}/.local/bin" \
  && echo "export PATH=${PATH}:${HOME}/.local/bin/" >> "${HOME}/.bash_profile" \
  && ln -s ~/.platformio/penv/bin/platformio ~/.local/bin/platformio \
  && ln -s ~/.platformio/penv/bin/pio ~/.local/bin/pio \
  && ln -s ~/.platformio/penv/bin/piodebuggdb ~/.local/bin/piodebuggdb
