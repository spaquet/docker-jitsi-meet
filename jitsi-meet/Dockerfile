FROM node:12.16.1-alpine3.11
LABEL maintainer="Dave Conroy <dave at tiredofit dot ca>"

ARG JITSIMEET_VERSION

### Set Environment Variables
ENV ENABLE_SMTP=FALSE
ENV JITSIMEET_VERSION=${JITSIMEET_VERSION:-2957}

### Add User
  RUN set -x ; \
      adduser -h /app -D -g "Jitsi Meet" -u 2500 jitsi ; \

### Add Dependencies
      apk update ; \
      apk add \
          git \
          nginx \
          make \
          ; \

### Fetch Jitsi Meet https://github.com/jitsi/jitsi-meet/archive/3931.zip
    curl -sSL https://github.com/jitsi/jitsi-meet/archive/3931.zip | tar xvfz - --strip 1 -C /app/ ; \
    cd /app ; \
### Install
    npm install node-sass@latest ; \
    npm install ; \
    make ; \

### Permissions Set
    chown -R jitsi /app ; \

### Cleanup
    apk del \
        git \
        make \
        ; \

    rm -rf /usr/src/* /var/cache/apk/* /tmp/* /var/tmp/*

### Networking Configuration
  EXPOSE 80 443 5280 5347

### Add Files
  ADD install /
