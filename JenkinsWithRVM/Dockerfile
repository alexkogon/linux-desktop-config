FROM jenkins:latest
MAINTAINER alko@j2medev.info

USER root

RUN apt-get update


# Install some dependencies
RUN apt-get -y -q install curl rubygems


# Install rvm
RUN curl -L https://get.rvm.io | bash -s stable

# Install package dependencies
RUN /usr/local/rvm/bin/rvm requirements

# Install ruby
RUN /usr/local/rvm/bin/rvm install ruby-2.3.3

# create first wrapper scripts
RUN /usr/local/rvm/bin/rvm wrapper ruby-2.3.3 myapp rake gem

RUN curl http://chromedriver.storage.googleapis.com/2.27/chromedriver_linux64.zip >chromedriver_linux64.zip
RUN unzip chromedriver_linux64.zip
RUN cp chromedriver /usr/local/bin/chromedriver

RUN apt-get -y install libxss1 libappindicator1 libindicator7 libpango1.0-0 fonts-liberation xdg-utils
RUN wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
RUN dpkg -i google-chrome*.deb

RUN apt-get install -y apt-utils
RUN apt-get install -y openssh-server
RUN mkdir /var/run/sshd
RUN /usr/sbin/sshd -D &

RUN echo 'root:screencast' | chpasswd


EXPOSE 22
