FROM jenkins/jenkins:lts-jdk21
LABEL org.opencontainers.image.authors="rgeoffroy@jusrionegro.gov.ar"
USER root
RUN apt-get update && \
    apt-get -y install apt-transport-https \
    sshpass \
    ca-certificates \
    curl \
    gnupg2 \
    software-properties-common && \
    curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg > /tmp/dkey; apt-key add /tmp/dkey && \
    add-apt-repository \
    "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
    $(lsb_release -cs) \
    stable" && \
    apt-get update && \
    apt-get -y install docker-ce
RUN apt-get install -y docker-ce
RUN curl -LO https://dl.k8s.io/release/v1.31.0/bin/linux/amd64/kubectl
RUN install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
RUN usermod -a -G docker jenkins
RUN echo "{ \"insecure-registries\":[\"registry-devops.jusrionegro.gov.ar:5000\"] }"
USER jenkins
