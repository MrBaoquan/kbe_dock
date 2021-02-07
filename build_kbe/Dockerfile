FROM ubuntu:18.04 AS kbe_build
LABEL maintainer="MrBaoquan <mrma617@gmail.com>"

ENV DEBIAN_FRONTEND=noninteractive

# USER root
RUN mirror_url=mirrors.aliyun.com && \
# ubuntu 20.04 LTS
sed -i "s/security.ubuntu.com/$mirror_url/" /etc/apt/sources.list && \
sed -i "s/archive.ubuntu.com/$mirror_url/" /etc/apt/sources.list && \
sed -i "s/security-cdn.ubuntu.com/$mirror_url/" /etc/apt/sources.list && \
apt-get update

RUN apt-get update \
  && apt install -y apt-utils \
  && apt install -y curl \
  && apt install -y libmysqlclient-dev \
  && apt install -y autoconf automake libtool libmysqlclient-dev \
  && apt install -y build-essential \
  && apt install -y vim \
  && apt install -y iputils-ping \
  && apt-get install -y python3-pip python3-dev \
  && cd /usr/local/bin \
  && ln -s /usr/bin/python3 python \
  && pip3 install --upgrade pip

#  编译安装 kbengine
COPY ./kbengine-2.5.11.tar.gz /home

WORKDIR /home

RUN tar -zxvf kbengine-2.5.11.tar.gz \
    && rm -f ./kbengine-2.5.11.tar.gz \
    && cd kbengine-2.5.11/kbe/src \
    && make \
    && cd ../ && rm -rf src

WORKDIR /home/kbengine-2.5.11

FROM scratch AS export
COPY --from=kbe_build /home/kbengine-2.5.11 .