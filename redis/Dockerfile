FROM centos:7
WORKDIR /opt
ARG Version=v2.1.0
ENV Version=${Version} \
    LANG=en_US.utf8

RUN set -ex \
    && yum install -y epel-release wget \
    && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "LANG=en_US.utf8" > /etc/locale.conf \
    && yum -y install redis \
    && yum remove -y wget \
    && sed -i "s/protected-mode yes/protected-mode no/g" /etc/redis.conf \
    && sed -i "s/bind 127.0.0.1/bind 0.0.0.0/g" /etc/redis.conf \
    && sed -i "561i maxmemory-policy allkeys-lru" /etc/redis.conf \
    && yum clean all \
    && rm -rf /var/cache/yum/*

COPY redis/entrypoint.sh .
RUN chmod 755 ./entrypoint.sh

CMD ["./entrypoint.sh"]
