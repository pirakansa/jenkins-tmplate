FROM jenkins/inbound-agent:3107.v665000b_51092-5-alpine-jdk11 as jnlp

###### Dockerfile
FROM golang:1.20-bullseye

###### Env 
ARG DEBIAN_FRONTEND=noninteractive
ARG USER=builder
ARG UID=1000

ENV DEBIAN_FRONTEND=noninteractive \
    LANG=C.UTF-8 \
    LANGUAGE=en_US:en \
    LC_ALL=C.UTF-8

COPY --from=jnlp /usr/local/bin/jenkins-agent /usr/local/bin/jenkins-agent
COPY --from=jnlp /usr/share/jenkins/agent.jar /usr/share/jenkins/agent.jar

###### Run
RUN apt update -y && \
    apt install -y --no-install-recommends default-jre-headless
RUN useradd -u ${UID} -s /bin/bash -m ${USER} && \
    usermod -G root ${USER} && \
    install --owner=${USER} --directory /work && \
    install --owner=${USER} --directory /.cache


# clear
RUN rm -rf /var/lib/apt/lists/* ; \
    rm -rf /var/cache/apt/archives/* ; \
    rm -rf /var/cache/apt/*.bin ; \
    rm -rf /var/cache/debconf/*-old ; \
    rm -rf /var/lib/dpkg/*-old ; \
    rm -rf /var/log/* ; \
    rm -rf /var/tmp/* ; \
    rm -rf /tmp/*

###### login user
USER ${USER}


ENTRYPOINT ["/usr/local/bin/jenkins-agent"]
