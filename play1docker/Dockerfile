FROM ubuntu:14.04

# Install.
# Install Python.
# Install Java.
RUN \
  apt-get update && \
  apt-get -y upgrade && \
  apt-get install -y software-properties-common && \
  apt-add-repository multiverse && \
  apt-get update && \
  apt-get -y upgrade && \
  apt-get install -y build-essential byobu curl git htop man unzip vim wget && \
  apt-get install -y python python-dev python-pip python-virtualenv && \
  echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
  add-apt-repository -y ppa:webupd8team/java && \
  apt-get update && \
  apt-get install -y oracle-java8-installer && \
  rm -rf /var/lib/apt/lists/* && \
  rm -rf /var/cache/oracle-jdk8-installer

# Define working directory.
WORKDIR /data

# Define commonly used JAVA_HOME variable
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

# Define application relative path
ENV PLAY_APP webapp

# Define application profile
ENV PLAY_PROFILE --%default

ENTRYPOINT ["/data/play/play"]

CMD start $PLAY_APP $PLAY_PROFILE
