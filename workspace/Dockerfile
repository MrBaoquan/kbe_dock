FROM ubuntu:18.04
LABEL maintainer="MrBaoquan <mrma617@gmail.com>"

ENV DEBIAN_FRONTEND=noninteractive


ARG TZ=UTC
ENV TZ ${TZ}

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
  && apt install -y vim \
  && apt install -y iputils-ping

WORKDIR /home/kbengine