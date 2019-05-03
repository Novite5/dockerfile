FROM ubuntu:16.04 


ARG BUILD_DATE
ARG VCS_REF
ARG VERSION
LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.name="Asuswrt Merlin Build" \
      org.label-schema.description="Asuswrt Merlin 固件交叉编译环境"

ENV ASUSWRT_MERLIN_VERSION 380.70

COPY build.sh /root/build.sh

COPY download_merlin.sh /root/download_merlin.sh 

RUN dpkg --add-architecture i386 \
    && sed -i -e 's/http:\/\/archive/http:\/\/cn\.archive/' /etc/apt/sources.list \
    && apt-get update -y \
    && apt-get install -y \
        sudo net-tools cron e2fsprogs wget vim openssl curl psmisc git \
        heirloom-mailx autoconf automake bison bzip2 bsdtar diffutils \
        sed file flex g++ gawk gcc-multilib gettext gperf groff-base \
        libncurses-dev libexpat1-dev libslang2 libssl-dev libtool \
        libxml-parser-perl make patch perl pkg-config python shtool tar \
        texinfo unzip zlib1g zlib1g-dev intltool autopoint libltdl7-dev \
        lib32z1-dev lib32stdc++6 automake1.11 libelf-dev:i386 libelf1:i386 \
    && apt-get autoremove -y \
    && apt-get autoclean -y \
    && rm -rf /var/lib/apt/lists/* \
    && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone \
    && echo ". ~/build.sh" >> /root/.bashrc 

CMD ["bash"]
