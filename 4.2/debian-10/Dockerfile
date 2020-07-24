FROM ubuntu:latest
#debian:stable
LABEL maintainer "Sad guy"

ENV HOME="/" \
    OS_ARCH="ppc64el" \
    OS_FLAVOUR="debian-10" \
    OS_NAME="linux"

COPY prebuildfs /
# Install required system packages and dependencies
#RUN install_packages acl ca-certificates curl gzip libc6 libcom-err2 libcurl4 libffi6 libgcc1 libgcrypt20 libgmp10 libgnutls30 libgpg-error0 libgssapi-krb5-2 libhogweed4 libidn2-0 libk5crypto3 libkeyutils1 libkrb5-3 libkrb5support0 libldap-2.4-2 libnettle6 libnghttp2-14 libp11-kit0 libpcap0.8 libpsl5 librtmp1 libsasl2-2 libssh2-1 libssl1.1 libtasn1-6 libunistring2 procps tar zlib1g
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
       # yq \
       # wait-for-port \
       # render-template \
        mongodb \
        gosu \
    && rm -rf /var/lib/apt/lists/*
#RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "yq" "3.3.2-0"
#RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "wait-for-port" "1.0.0-1"
#RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "render-template" "1.0.0-1"
#RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "mongodb" "4.2.8-0"
#RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "gosu" "1.12.0-1"

RUN apt-get update && apt-get upgrade -y && \
    rm -r /var/lib/apt/lists /var/cache/apt/archives
RUN chmod g+rwX /opt/bitnami

COPY rootfs /
RUN /opt/bitnami/scripts/mongodb/postunpack.sh
ENV BITNAMI_APP_NAME="mongodb" \
    BITNAMI_IMAGE_VERSION="4.2.8-debian-10-r40" \
    PATH="/opt/bitnami/common/bin:/opt/bitnami/mongodb/bin:$PATH"

EXPOSE 27017

USER 1001
ENTRYPOINT [ "/opt/bitnami/scripts/mongodb/entrypoint.sh" ]
CMD [ "/opt/bitnami/scripts/mongodb/run.sh" ]
