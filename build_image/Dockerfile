FROM debian:11-slim AS builder
RUN apt-get update && apt-get install -y wget curl tar 
COPY get_xui_release.sh .
RUN bash get_xui_release.sh

FROM debian:11-slim
LABEL org.opencontainers.image.authors="https://github.com/Chasing66"
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get install -y --no-install-recommends -y ca-certificates \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
ENV TZ=Asia/Shanghai
WORKDIR /usr/local/x-ui
COPY --from=builder  /usr/local/x-ui/ /usr/local/x-ui/
VOLUME [ "/etc/x-ui" ]
CMD [ "./x-ui" ]