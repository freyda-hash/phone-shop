FROM jenkins/jenkins:2.516.1-lts-jdk21

USER root

RUN apt-get update \
    && apt-get install -y docker.io docker-compose-plugin \
    && rm -rf /var/lib/apt/lists/*

USER jenkins
