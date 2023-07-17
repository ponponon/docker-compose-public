FROM python:3.10.10-bullseye 
RUN . /etc/os-release && cat > /etc/apt/sources.list <<EOF
    deb http://mirrors.tuna.tsinghua.edu.cn/debian/ ${VERSION_CODENAME} main contrib non-free
    deb http://mirrors.tuna.tsinghua.edu.cn/debian/ ${VERSION_CODENAME}-updates main contrib non-free
    deb http://mirrors.tuna.tsinghua.edu.cn/debian/ ${VERSION_CODENAME}-backports main contrib non-free
    deb http://security.debian.org/debian-security bullseye-security main contrib non-free
EOF

RUN apt-get update
RUN apt-get install -y vim
RUN apt-get install -y openjdk-11-jre
RUN echo "export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-arm64" | tee -a /etc/profile >/dev/null
RUN apt-get install -y wget
WORKDIR /root
RUN wget -P /root https://dlcdn.apache.org/hbase/2.4.17/hbase-2.4.17-src.tar.gz
RUN tar xvf /root/hbase-2.4.17-src.tar.gz

