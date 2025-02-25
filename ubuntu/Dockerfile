FROM ubuntu:jammy

USER root
WORKDIR /root

ARG ROOT_VERSION=6.28.10

# configure system
COPY . /root
RUN apt-get update -qq && \
    ln -sf /usr/share/zoneinfo/UTC /etc/localtime && \
    DEBIAN_FRONTEND="noninteractive" apt-get -y install $(cat packages) && \
    locale-gen en_US.UTF-8 && update-locale && \
    rm -rf /var/lib/apt/lists/*

ENV LC_ALL="en_US.utf8" \
    LANGUAGE="en_US.utf8" \
    LANG="en_US.utf8"

# default python
RUN update-alternatives --install /usr/bin/python python /usr/bin/python3 1 && \
    update-alternatives --install /usr/bin/pip pip /usr/bin/pip3 1

RUN mkdir -p /opt/root && \
    wget -q -O- "https://root.cern/download/root_v${ROOT_VERSION}.Linux-ubuntu22-x86_64-gcc11.4.tar.gz" \
        | tar --strip-components 1 -C /opt/root --strip=1 -x -z

ENV ROOTSYS="/opt/root" \
    PATH="$PATH:/opt/root/bin" \
    LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/opt/root/lib" \
    MANPATH="$MANPATH:/opt/root/man" \
    PYTHONPATH="$PYTHONPATH:/opt/root/lib" \
    JUPYTER_CONFIG_DIR="$JUPYTER_CONFIG_DIR:/opt/root/etc/notebook" \
    CLING_STANDARD_PCH="none"
