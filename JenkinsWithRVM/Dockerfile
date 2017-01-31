FROM jenkins:alpine
MAINTAINER alko@j2medev.info

USER root

RUN apk update


# Install some dependencies
RUN apk -y -q add curl rubygems


# Install rvm
RUN curl -L https://get.rvm.io | bash -s stable

# Install package dependencies
RUN /usr/local/rvm/bin/rvm requirements

# Install ruby
RUN /usr/local/rvm/bin/rvm  ruby-2.3.3

# create first wrapper scripts
RUN /usr/local/rvm/bin/rvm wrapper ruby-2.3.3 myapp rake gem

RUN curl http://chromedriver.storage.googleapis.com/2.27/chromedriver_linux64.zip >chromedriver_linux64.zip
RUN unzip chromedriver_linux64.zip
RUN cp chromedriver /usr/local/bin/chromedriver

RUN apk -y  libxss1 libappindicator1 libindicator7 libpango1.0-0 fonts-liberation xdg-utils
RUN wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
RUN dpkg -i google-chrome*.deb

EXPOSE 22
