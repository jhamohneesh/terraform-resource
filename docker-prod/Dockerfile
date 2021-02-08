FROM alpine:latest

RUN apk update && \
    apk add ca-certificates git bash openssh-client

RUN wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub && \
  wget -q -O /tmp/glibc.apk https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.32-r0/glibc-2.32-r0.apk && \
  apk add /tmp/glibc.apk && \
  rm -rf /tmp/glibc.apk

RUN mkdir -p $HOME/.ssh
RUN echo "StrictHostKeyChecking no" >> $HOME/.ssh/config
RUN echo "LogLevel quiet" >> $HOME/.ssh/config
RUN chmod 0600 $HOME/.ssh/config

RUN if [ `uname -m` = "aarch64" ] ; then \
           arch="arm64"; \
    else \
           arch="amd64"; \
    fi && \
    mkdir -p /usr/local/share/terraform/plugins/github.com/ashald/stateful/1.2.0/linux_$arch/ && \
    wget -O /usr/local/share/terraform/plugins/github.com/ashald/stateful/1.2.0/linux_$arch/terraform-provider-stateful_v1.2.0 \
    "https://github.com/ashald/terraform-provider-stateful/releases/download/v1.2.0/terraform-provider-stateful_v1.2.0-linux-$arch" && \
    chmod +x /usr/local/share/terraform/plugins/github.com/ashald/stateful/1.2.0/linux_$arch/terraform-provider-stateful_v1.2.0
COPY terraform/* /usr/local/bin/
COPY check in out /opt/resource/
