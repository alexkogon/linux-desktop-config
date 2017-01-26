FROM jenkins:alpine
MAINTAINER alko@j2medev.info

USER root

RUN apk update


# Install some dependencies
RUN apk -y -q install curl rubygems


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

RUN apk -y install libxss1 libappindicator1 libindicator7 libpango1.0-0 fonts-liberation xdg-utils
RUN wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
RUN dpkg -i google-chrome*.deb

RUN apk install -y apt-utils
RUN apk install -y openssh-server
RUN mkdir /var/run/sshd

RUN echo 'root:screencast' | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile
RUN /usr/sbin/sshd -D &

EXPOSE 22
