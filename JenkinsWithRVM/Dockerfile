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

RUN gem install rake
RUN gem install bundler