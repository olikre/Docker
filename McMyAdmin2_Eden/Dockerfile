FROM ubuntu:18.04
LABEL maintainer "oliver.krebs@me.com"

EXPOSE	8080
EXPOSE	25565
EXPOSE	8123

ARG DEBIAN_FRONTEND="noninteractive"

RUN	apt-get update && \
	apt-get -y upgrade && \
	apt-get -y install wget openjdk-8-jdk-headless unzip libgdiplus && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/* 
		
WORKDIR	/usr/local
RUN	wget http://mcmyadmin.com/Downloads/etc.zip && \
	unzip etc.zip && rm etc.zip

WORKDIR	/home/mcmyadmin
RUN	wget http://mcmyadmin.com/Downloads/MCMA2_glibc26_2.zip && \
	unzip MCMA2_glibc26_2.zip && rm MCMA2_glibc26_2.zip

ADD	McMyAdmin.conf /home/mcmyadmin/McMyAdmin.conf
ADD eula.txt /home/mcmyadmin/Minecraft/eula.txt
ADD	start.sh /start.sh
RUN	chmod 755 /start.sh

RUN	/home/mcmyadmin/MCMA2_Linux_x86_64 -nonotice -updateonly

CMD	["/start.sh"]
