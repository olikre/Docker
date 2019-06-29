#Datei Dockerfile
FROM ubuntu:18.04
LABEL maintainer "oliver.krebs@me.com"
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
CMD ["/bin/bash"]