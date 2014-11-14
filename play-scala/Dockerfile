# Ubuntu 14.04 is base image
FROM ubuntu:14.04

# Update platform to prepare for Java installation
RUN sed 's/main$/main universe/' -i /etc/apt/sources.list
RUN apt-get update && apt-get install -y software-properties-common python-software-properties
RUN add-apt-repository ppa:webupd8team/java -y
RUN apt-get update
RUN echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections

# Install Java 7
RUN apt-get install -y oracle-java7-installer

# Install unzip
RUN sudo apt-get install unzip

# Add and unzip the Play app
ADD path/to/my-play-artifact-1.0-SNAPSHOT.zip /opt/my-play-artifact-1.0-SNAPSHOT.zip
RUN unzip /opt/my-play-artifact-1.0-SNAPSHOT.zip -d /opt

# Give exec permission to the start script (unzip doesn't preserve permissions)
RUN chmod 755 /opt/my-play-artifact/bin/my-play-artifact

#play port to expose
EXPOSE 9000

# start the Play! app on port 9000
CMD nohup /opt/my-play-artifact/bin/my-play-artifact -Dhttp.port=9000
