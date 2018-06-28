FROM ubuntu:17.10

## General package configuration
RUN apt-get -y update && \
         apt-get -y install \
         sudo \
         unzip \
         curl \
         xmlstarlet \
         git \
         netcat-traditional \
         software-properties-common \
         debconf-utils \
         uuid-runtime \
         ncurses-bin \
         iputils-ping \
         net-tools \
         zip \
         openssh-server \
         openssh-client \
         apt-transport-https \
         wget \
         vim \
         ssh \
         python \
         docker.io

## Install Java
#RUN \
# add-apt-repository -y ppa:openjdk-r/ppa  && \
# apt-get update && \
# apt-get install -y openjdk-8-jdk
RUN apt-get install default-jre -y



#Install PS
RUN curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
RUN curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/17.04/prod.list
RUN apt-get update
RUN apt-get install -y libicu57
RUN apt-get install -y powershell



# Installing rundeck
RUN curl https://bintray.com/user/downloadSubjectPublicKey?username=bintray > bintray.key
RUN cat bintray.key | apt-key add -
RUN echo "deb https://rundeck.bintray.com/rundeck-deb /" | sudo tee -a /etc/apt/sources.list
RUN apt-get -y update
RUN apt-get -y install rundeck


# add cli tool debian repo
ARG CLI_DEB_URL=https://dl.bintray.com/rundeck/rundeck-deb
RUN echo "deb $CLI_DEB_URL /" | sudo tee -a /etc/apt/sources.list
RUN apt-get -y update
RUN apt-get -y install rundeck-cli


ENV USERNAME=rundeck \
    USER=rundeck \
    HOME=/rundeck-install \
    RDECK_BASE=/var/lib/rundeck

WORKDIR $HOME

RUN echo "rundeck:rundeck" | chpasswd
RUN usermod -a -G root rundeck

RUN mkdir -p $HOME
RUN mkdir -p $HOME/data
RUN mkdir -p $HOME/scripts
RUN mkdir -p $HOME/plugins

COPY data $HOME/data
COPY scripts $HOME/scripts
RUN chmod -R a+x $HOME/scripts/*

#copy plugins
COPY plugins $HOME/plugins
RUN chown -R $USER:$USER $HOME/plugins
COPY plugins/*.* $RDECK_BASE/libext/

#copy acls
COPY data/acl/*.* /etc/rundeck
RUN chown -R $USER:$USER /etc/rundeck


EXPOSE 4440
CMD $HOME/scripts/run
