FROM debian:bookworm

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update \
    && apt-get install -y \
        curl \
        gnupg2 \
        apt-transport-https \
    && echo "deb [signed-by=/etc/apt/keyrings/auth-49-pub.asc arch=amd64] http://repo.powerdns.com/debian bookworm-auth-49 main" > /etc/apt/sources.list.d/pdns.list \
    && install -d /etc/apt/keyrings \
    && curl https://repo.powerdns.com/FD380FBB-pub.asc | tee /etc/apt/keyrings/auth-49-pub.asc \
    && apt-get update \
    && apt-get install -y \
        pdns-server \
        pdns-backend-bind \
        pdns-tools \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

EXPOSE 53
EXPOSE 8081

CMD [ "/usr/sbin/pdns_server", "--guardian=no", "--daemon=no", "--disable-syslog", "--log-timestamp=no", "--write-pid=no" ]