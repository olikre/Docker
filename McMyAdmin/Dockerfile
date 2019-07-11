FROM ubuntu:18.04
LABEL maintainer "oliver.krebs@me.com"

EXPOSE	8080
EXPOSE	25565
EXPOSE	8123

ARG DEBIAN_FRONTEND="noninteractive"

RUN	apt-get update && \
	apt-get -y upgrade && \
	apt-get -y install curl openjdk-8-jdk-headless unzip libgdiplus && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/* 
		
WORKDIR	/usr/local
RUN	curl -o http://mcmyadmin.com/Downloads/etc.zip && \
	unzip etc.zip && rm etc.zip

WORKDIR	/home/mcmyadmin
RUN	curl -o http://mcmyadmin.com/Downloads/MCMA2_glibc26_2.zip && \
	unzip MCMA2_glibc26_2.zip && rm MCMA2_glibc26_2.zip

WORKDIR	/home/mcmyadmin/Minecraft
RUN echo 'eula=true' > /home/mcmyadmin/Minecraft/eula.txt

RUN echo '#!/bin/sh' > /start.sh && \
    echo 'FILE=/home/mcmyadmin/pass.txt' >> /start.sh && \
    echo 'if [ -z $JAVA_MEMORY ]; then' >> /start.sh && \
    echo '   JAVA_MEMORY=2048' >> /start.sh && \
    echo 'fi' >> /start.sh && \
    echo 'if [ -f "$FILE" ]; then' >> /start.sh && \
    echo '   /home/mcmyadmin/MCMA2_Linux_x86_64 +java.memory $JAVA_MEMORY' >> /start.sh && \
    echo 'else' >> /start.sh && \
    echo '   /home/mcmyadmin/MCMA2_Linux_x86_64 -setpass admin +java.memory $JAVA_MEMORY' >> /start.sh && \
    echo '   touch $FILE' >> /start.sh && \
    echo 'fi' >> /start.sh

RUN	chmod 755 /start.sh

RUN	/home/mcmyadmin/MCMA2_Linux_x86_64 -nonotice -updateonly -setpass test1234 

CMD	["/start.sh"]
