FROM ubuntu:jammy
RUN . /etc/os-release && cat > /etc/apt/sources.list <<EOF
    deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ ${VERSION_CODENAME} main restricted universe multiverse
    deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ ${VERSION_CODENAME}-updates main restricted universe multiverse
    deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ ${VERSION_CODENAME}-backports main restricted universe multiverse
    deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ ${VERSION_CODENAME}-security main restricted universe multiverse
EOF

RUN apt update
RUN apt install -y vim gcc g++ cmake make
RUN apt install -y redis-server
CMD ["redis-server", "/etc/redis/redis.conf"]