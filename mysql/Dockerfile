FROM mysql:5.7

RUN export DEBIAN_FRONTEND=noninteractive \
    && apt-get install -y tzdata

RUN rm -rf /etc/localtime \
    && ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && dpkg-reconfigure -f noninteractive tzdata