FROM bitnami/minideb-extras-base:stretch-r362
LABEL maintainer "Bitnami <containers@bitnami.com>"

ENV BITNAMI_PKG_CHMOD="-R g+rwX" \
    HOME="/" \
    OS_ARCH="amd64" \
    OS_FLAVOUR="debian-9" \
    OS_NAME="linux"

# Install required system packages and dependencies
RUN install_packages libaio1 libaudit1 libc6 libcap-ng0 libgcc1 libjemalloc1 libncurses5 libpam0g libssl1.0.2 libstdc++6 libtinfo5 zlib1g
RUN . ./libcomponent.sh && component_unpack "mariadb" "10.3.18-0" --checksum 01062cf4a250782445895dea5bc3da3b7ceb9d4f923c5b4ee60d2dc50c2999b6
RUN mkdir /docker-entrypoint-initdb.d
ADD ejercicio3.sql /docker-entrypoint-initdb.d/ejercicio3.sql
RUN chmod -R 775 /docker-entrypoint-initdb.d

COPY rootfs /
RUN /postunpack.sh
ENV BITNAMI_APP_NAME="mariadb" \
    BITNAMI_IMAGE_VERSION="10.3.18-debian-9-r4" \
    NAMI_PREFIX="/.nami" \
    PATH="/opt/bitnami/mariadb/bin:/opt/bitnami/mariadb/sbin:$PATH"

EXPOSE 3306

USER 1001
ENTRYPOINT [ "/entrypoint.sh" ]
CMD [ "/run.sh" ]
