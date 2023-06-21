FROM debian:bookworm
RUN . /etc/os-release && cat > /etc/apt/sources.list <<EOF
    deb http://mirrors.tuna.tsinghua.edu.cn/debian/ ${VERSION_CODENAME} main contrib non-free
    deb http://mirrors.tuna.tsinghua.edu.cn/debian/ ${VERSION_CODENAME}-updates main contrib non-free
    deb http://mirrors.tuna.tsinghua.edu.cn/debian/ ${VERSION_CODENAME}-backports main contrib non-free
EOF

RUN apt-get update
RUN apt-get install -y wget mycli htop vim netcat telnet sysstat httpie libgl1-mesa-dev ffmpeg libsm6 libxext6 less

RUN mkdir /code
RUN mkdir -p /code/logs
WORKDIR /code
