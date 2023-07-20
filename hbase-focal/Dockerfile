# syntax=docker/dockerfile:1

# x86 架构
FROM ubuntu:focal AS base_focal

RUN if [ "$TARGETPLATFORM" = "linux/amd64" ]; then \
    . /etc/os-release && cat << EOF > /etc/apt/sources.list \
    deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse \
    deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse \
    deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse \
    deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse \
    EOF \
    ; fi

RUN if [ "$TARGETPLATFORM" = "linux/arm64" ]; then \
    . /etc/os-release && cat << EOF > /etc/apt/sources.list \
    deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ focal main restricted universe multiverse \
    deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ focal-updates main restricted universe multiverse \
    deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ focal-backports main restricted universe multiverse \
    deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ focal-security main restricted universe multiverse \
    EOF \
    ; fi



RUN apt-get update
RUN apt-get install -y vim
RUN apt-get install -y openjdk-8-jdk

RUN apt-get install -y wget
WORKDIR /root
RUN wget -P /root https://mirrors.tuna.tsinghua.edu.cn/apache/hbase/2.4.17/hbase-2.4.17-bin.tar.gz
RUN tar xvf /root/hbase-2.4.17-bin.tar.gz

ARG TARGETPLATFORM
ENV TARGETPLATFORM=${TARGETPLATFORM}

ARG TARGETARCH
ENV TARGETARCH=${TARGETARCH}

ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-${TARGETARCH}


COPY entrypoint.sh /root/
RUN chmod +x /root/entrypoint.sh

CMD ["/root/entrypoint.sh"]