FROM python:3.10.10-bullseye 
RUN . /etc/os-release && cat > /etc/apt/sources.list <<EOF
    deb http://mirrors.tuna.tsinghua.edu.cn/debian/ ${VERSION_CODENAME} main contrib non-free
    deb http://mirrors.tuna.tsinghua.edu.cn/debian/ ${VERSION_CODENAME}-updates main contrib non-free
    deb http://mirrors.tuna.tsinghua.edu.cn/debian/ ${VERSION_CODENAME}-backports main contrib non-free
    deb http://security.debian.org/debian-security bullseye-security main contrib non-free
EOF

RUN apt-get update
RUN apt-get install -y vim
RUN apt-get install -y openjdk-17-jdk
