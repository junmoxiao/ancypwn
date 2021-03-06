FROM ubuntu:20.04

MAINTAINER Anciety <anciety512@gmail.com>

COPY ./get-pip.py /root/get-pip.py

# Apt packages
RUN dpkg --add-architecture i386 && apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -qy \
    git nasm python3 \
    build-essential \
    python3-dev python3-setuptools && \
    python3 /root/get-pip.py && \
    DEBIAN_FRONTEND=noninteractive apt-get install -qy \
    libc6-dbg \
    libc6-dbg:i386 \
    gcc-multilib \
    gdb-multiarch \
    gcc \
    wget \
    curl \
    glibc-source \
    cmake \
    python-capstone \
    socat \
    netcat \
    ruby \
    ruby-dev \
    lxterminal && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    cd ~ && tar -xf /usr/src/glibc/glibc-*.tar.xz

# python/ruby packages & gdb-plugin
RUN pip3 install --no-cache-dir pwntools ropper ancypatch && \
    gem install one_gadget seccomp-tools && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# git installaing package
RUN cd ~/ && \
    git clone https://github.com/pwndbg/pwndbg.git && \
    cd ~/pwndbg/ && ./setup.sh && \
    cd ~/ && \
    git clone https://github.com/junmoxiao/Pwngdb && \
    cp ~/Pwngdb/.gdbinit ~/ && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV LANG C.UTF-8

COPY ./ancyterm.py /usr/local/bin/ancyterm
RUN chmod +x /usr/local/bin/ancyterm

VOLUME ["/pwn"]
WORKDIR /pwn

CMD ["/bin/bash"]
