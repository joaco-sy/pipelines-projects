FROM jenkins/jenkins:lts
USER root
RUN apt-get update -qq \
    && apt-get install -qqy apt-trasport-https ca-certificates curl gnupg software-properties-common wget
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
RUN add-apt-repository \
    "deb [arch=amd64] https://download.docker.com/linux/debian \
    $(lsb_release -cs) \
    stable"
RUN apt-get update -qq \
    && apt-get -y install docker-ce
RUN usermod -aG docker jenkins
USER jenkins