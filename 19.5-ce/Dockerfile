# Copyright (c) 2020, 2022 Oracle and/or its affiliates.
# Licensed under the Universal Permissive License v 1.0 as shown at https://oss.oracle.com/licenses/upl/
#
FROM openjdk:14-oraclelinux7

LABEL org.opencontainers.image.source = "https://github.com/oracle/docker-images"

ENV VERSION="19.5.25" \
    KVHOME=/kv-19.5.25 \
    PACKAGE="kv-ce" \
    EXTENSION="zip" \
    BASE_URL="http://download.oracle.com/otn-pub/otn_software/nosql-database/" \
    _JAVA_OPTIONS="-Djava.security.egd=file:/dev/./urandom"

RUN yum -y install unzip && \
    curl -OLs "${BASE_URL}/${PACKAGE}-${VERSION}.${EXTENSION}" && \
    unzip "${PACKAGE}-${VERSION}.${EXTENSION}" && \
    rm "${PACKAGE}-${VERSION}.${EXTENSION}" && \
    yum -y remove unzip && rm -rf /var/cache/yum/*

VOLUME ["/kvroot"]

WORKDIR "$KVHOME"

EXPOSE 5000 5001 5010-5020

CMD ["java", "-jar", "lib/kvstore.jar", "kvlite", "-secure-config", "disable", "-root", "/kvroot"]
