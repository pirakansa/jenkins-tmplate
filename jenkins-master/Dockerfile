FROM jenkins/jenkins:2.402-alpine-jdk17

###### Env 

ENV DEBIAN_FRONTEND=noninteractive \
    LANG=C.UTF-8 \
    LANGUAGE=en_US:en \
    LC_ALL=C.UTF-8 \
    JAVA_OPTS="-Djenkins.install.runSetupWizard=false -Djava.net.useSystemProxies=true" \
    CASC_JENKINS_CONFIG=/config/jenkins.yaml


COPY ./config/jenkins.yaml /config/jenkins.yaml
COPY ./config/plugins.txt  /config/plugins.txt

# if we want to install via apt
USER root
RUN /bin/jenkins-plugin-cli --plugin-file /config/plugins.txt


# drop back to the regular jenkins user - good practice
USER jenkins
