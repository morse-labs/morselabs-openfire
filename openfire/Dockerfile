FROM alpine

LABEL maintainer Nick Byrne <nick@morselabs.net>

ARG OPENFIRE_VERSION_ARG=4_9_1
ARG BUILD_VERSION_ARG=1.0
ARG BUILD_DATE_ARG=24-10-24

ENV OPENFIRE_VERSION=${OPENFIRE_VERSION_ARG}
ENV BUILD_VERSION=${BUILD_VERSION_ARG}
ENV BUILD_DATE=${BUILD_DATE_ARG}

LABEL maintainer Nick Byrne <nick@morselabs.net>
LABEL org.label-schema.name="Openfire"
LABEL org.label-schema.description="Openfire is a real time collaboration (RTC) server supporting XMPP messaging"
LABEL org.label-schema.url="https://www.igniterealtime.org/projects/openfire/"
LABEL org.label-schema.application="openfire"
LABEL org.label-schema.build-date=$BUILD_DATE
LABEL org.label-schema.version=$BUILD_VERSION

RUN set -ex \
 && apk --no-cache add \
      bash \
      ca-certificates \
      curl \
      openjdk11 \
 && mkdir -p /opt \
 && curl -sSfL "https://www.igniterealtime.org/downloadServlet?filename=openfire/openfire_${OPENFIRE_VERSION}.tar.gz" | \
      tar -xz -C /opt \
 && curl -sSfLo /usr/local/bin/dumb-init https://github.com/Yelp/dumb-init/releases/download/v1.2.1/dumb-init_1.2.1_amd64 \
 && chmod +x /usr/local/bin/dumb-init

ADD start.sh /usr/local/bin/start.sh

EXPOSE 9090 9091 5222 5223 5269
VOLUME ["/data"]

ENTRYPOINT ["/usr/local/bin/start.sh"]

