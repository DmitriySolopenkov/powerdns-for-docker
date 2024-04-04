FROM debian:buster-20240311

ENV DEBIAN_FRONTEND noninteractive

SHELL ["/bin/bash", "-exo", "pipefail", "-c"]

COPY src/ /

RUN apt-get update ;\
    apt-get -y install --no-install-recommends \
        curl \
        gnupg; \
    install -d /etc/apt/keyrings; curl https://repo.powerdns.com/FD380FBB-pub.asc | tee /etc/apt/keyrings/auth-49-pub.asc;\
    apt-get update ;\
    apt-get install -y --no-install-recommends \
        pdns-server \
        pdns-backend-bind \
        pdns-tools ;\
    apt-get clean ;\
    rm -rf /var/lib/apt/lists/*

EXPOSE 53
EXPOSE 8081

CMD [ "/usr/sbin/pdns_server", "--guardian=no", "--daemon=no", "--disable-syslog", "--log-timestamp=no", "--write-pid=no" ]