FROM debian:buster-20240311

ENV PDNS_REPO http://repo.powerdns.com/debian buster-auth-49 main

SHELL ["/bin/bash", "-exo", "pipefail", "-c"]

RUN apt-get update ;\
    apt-get -y install \
        tzdata \
        gnupg; \
    echo "deb $PDNS_REPO /" > /etc/apt/sources.list.d/bareos.list ;\
    install -d /etc/apt/keyrings; \
    curl https://repo.powerdns.com/FD380FBB-pub.asc | tee /etc/apt/keyrings/auth-49-pub.asc ;\
    apt-get update ;\
    apt-get install \
        pdns-server=4.9.0-1pdns.buster \
        pdns-backend-bind=4.9.0-1pdns.buster ;\
    apt-get clean ;\
    rm -rf /var/lib/apt/lists/*

EXPOSE 53
EXPOSE 8081

CMD [ "/usr/sbin/pdns_server", "--guardian=no", "--daemon=no", "--disable-syslog", "--log-timestamp=no", "--write-pid=no" ]