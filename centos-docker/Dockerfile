FROM centos:7
MAINTAINER nkano

# note
# use this image by sharing the host's docker daemon
# "-v /var/run/docker.sock:/var/run/docker.sock"

# install docker
RUN yum install -y yum-utils && \
    yum-config-manager \
        --add-repo \
        https://download.docker.com/linux/centos/docker-ce.repo && \
    yum makecache fast && \
    yum install -y docker-ce

# install docker-compose
RUN curl -L https://github.com/docker/compose/releases/download/1.13.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
RUN chmod +x /usr/local/bin/docker-compose

# install basic tools
RUN yum install -y net-tools bridge-utils zip unzip git

# install aws cli
RUN curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py" &&\
    python get-pip.py &&\
    pip install awscli
