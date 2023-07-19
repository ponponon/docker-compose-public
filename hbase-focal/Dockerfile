# syntax=docker/dockerfile:1

# x86 架构
FROM ubuntu:focal AS x86

RUN . /etc/os-release && cat > /etc/apt/sources.list <<EOF
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse
EOF

RUN apt-get update && apt-get install -y vim openjdk-8-jdk wget
WORKDIR /root
RUN wget -P /root https://mirrors.tuna.tsinghua.edu.cn/apache/hbase/2.4.17/hbase-2.4.17-bin.tar.gz
RUN tar xvf /root/hbase-2.4.17-bin.tar.gz

RUN echo "export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64" | tee -a /etc/profile >/dev/null
ENV JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64"
COPY entrypoint.sh /root/

# ARM 架构
FROM ubuntu:focal AS arm

RUN . /etc/os-release && cat > /etc/apt/sources.list <<EOF
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ focal main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ focal-updates main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ focal-backports main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ focal-security main restricted universe multiverse
EOF

RUN apt-get update && apt-get install -y vim openjdk-8-jdk wget
WORKDIR /root
RUN wget -P /root https://mirrors.tuna.tsinghua.edu.cn/apache/hbase/2.4.17/hbase-2.4.17-bin.tar.gz
RUN tar xvf /root/hbase-2.4.17-bin.tar.gz

RUN echo "export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-arm64" | tee -a /etc/profile >/dev/null
ENV JAVA_HOME="/usr/lib/jvm/java-8-openjdk-arm64"
COPY entrypoint.sh /root/

FROM --platform=$BUILDPLATFORM $TARGETPLATFORM AS final
COPY --from=final / /

# 定义入口点
CMD ["/root/entrypoint.sh"]
