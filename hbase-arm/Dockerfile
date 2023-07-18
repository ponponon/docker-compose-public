FROM ubuntu:focal
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

# docker run --rm -it ponponon/hbase-arm bash
# cd /root/hbase-2.4.17
# JAVA_HOME=/usr/lib/jvm/java-8-openjdk-arm64 bash bin/hbase-daemon.sh start master 