FROM python:latest
MAINTAINER nkano

# install nltk
RUN pip install -U nltk && \
    pip install -U numpy

# install praw
RUN pip install -U praw

# install convenient tools
RUN apt-get update &&\
    apt-get install -y net-tools bridge-utils zip unzip