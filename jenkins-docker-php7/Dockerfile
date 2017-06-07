FROM jenkins:latest
MAINTAINER nkano

USER root
WORKDIR /root

# install basic utils
RUN apt-get update && apt-get install -y --no-install-recommends \
                apt-utils \
                net-tools \
                rsync \
                zip \
                vim \
                sshpass \
                sudo

# add apt repository for php7.x installation
RUN apt-key adv --keyserver keys.gnupg.net --recv-keys 14AA40EC0831756756D7F66C4F4EA0AAE5267A6C; \
    echo "deb http://ppa.launchpad.net/ondrej/php/ubuntu trusty main" >> /etc/apt/sources.list; \
    echo "deb-src http://ppa.launchpad.net/ondrej/php/ubuntu trusty main" >> /etc/apt/sources.list;

# install php7.1
RUN apt-get update && apt-get install -y --no-install-recommends \
                php7.1 \
                php7.1-dev \
                php7.1-curl \
                php7.1-intl \
                php7.1-mbstring \
                phpunit \
                php-phalcon

# install docker
RUN apt-get install -y --no-install-recommends \
                apt-transport-https \
                ca-certificates \
                curl \
                gnupg2 \
                software-properties-common
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -; \
    add-apt-repository \
        "deb [arch=amd64] https://download.docker.com/linux/debian \
        $(lsb_release -cs) \
        stable"; \
    apt-get update; \
    apt-get install -y docker-ce

# install aws-cli
RUN curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py" && \
    python get-pip.py && \
    pip install awscli

# so jenkins can sudo without password
RUN echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers

# become jenkins user from now on
USER jenkins

### add initial jenkins data if you like
# ADD jenkins_home.tar.gz /var/
# RUN sudo chown -R jenkins /var/jenkins_home

### aws account login
# ADD config/.aws/* /var/jenkins_home/.aws/
# ADD config/.aws/* /root/.aws/
# RUN sudo chown -R jenkins /var/jenkins_home/.aws && \
#     sudo chmod 770 /var/jenkins_home/.aws/*

### github.com ssh connection
# ADD config/.ssh/* /var/jenkins_home/.ssh/
# RUN sudo chown -R jenkins /var/jenkins_home/.ssh &&\
#     sudo chmod 600 /var/jenkins_home/.ssh/* &&\
#     ssh -T -o StrictHostKeyChecking=no git@github.com ; exit 0