# syntax=docker/dockerfile:1

# x86 架构
FROM ubuntu:focal AS x86

RUN . /etc/os-release && cat > /etc/apt/sources.list <<EOF
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse
EOF

RUN apt-get update
RUN apt-get install -y vim
RUN apt-get install -y openjdk-8-jdk

RUN apt-get install -y wget
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

RUN apt-get update
RUN apt-get install -y vim
RUN apt-get install -y openjdk-8-jdk

RUN apt-get install -y wget
WORKDIR /root
RUN wget -P /root https://mirrors.tuna.tsinghua.edu.cn/apache/hbase/2.4.17/hbase-2.4.17-bin.tar.gz
RUN tar xvf /root/hbase-2.4.17-bin.tar.gz

RUN echo "export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-arm64" | tee -a /etc/profile >/dev/null
ENV JAVA_HOME="/usr/lib/jvm/java-8-openjdk-arm64"
COPY entrypoint.sh /root/

# 构建多平台镜像
FROM --platform=$BUILDPLATFORM x86 AS x86-platform
FROM --platform=$BUILDPLATFORM arm AS arm-platform

# 根据不同平台选择构建结果
FROM x86-platform AS final
# 或者使用下面的语法，选择 ARM 平台构建结果
# FROM arm-platform AS final

# 继续构建后续指令
# ...

# 定义入口点
CMD ["/root/entrypoint.sh"]
