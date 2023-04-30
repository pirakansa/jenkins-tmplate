FROM jenkins/ssh-agent:4.15.0-alpine-jdk17

###### Env 
ARG DOCKERID
ARG ARCH
ARG DOCKER_VERSION

ENV DEBIAN_FRONTEND=noninteractive \
    LANG=C.UTF-8 \
    LANGUAGE=en_US:en \
    LC_ALL=C.UTF-8

# if we want to install via apt
USER root
RUN wget -O docker.tgz "https://download.docker.com/linux/static/test/${ARCH:?}/docker-${DOCKER_VERSION:?}.tgz" \
    && tar --strip-components=1 -xvzf docker.tgz -C /usr/bin && rm -f docker.tgz \
    && grep -q ":${DOCKERID:?}:" /etc/group || addgroup -g ${DOCKERID:?} docker ; \
    adduser jenkins $(grep ":${DOCKERID:?}:" /etc/group | cut -d ":" -f 1) ;
