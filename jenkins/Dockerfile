FROM jenkins/jenkins:latest

LABEL MAINTAINER="Thanh Nam <nam.tt@neo-lab.vn>"

USER root

RUN apt-get update && apt-get install -y \
  apt-transport-https \
  software-properties-common

RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
RUN add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu xenial stable"

RUN apt-get update && apt-get install -y \
  docker-ce \
  vim \
  build-essential

RUN \
  apt-get update && apt-get install -y --no-install-recommends --no-install-suggests curl bzip2 build-essential libssl-dev libreadline-dev zlib1g-dev && \
  rm -rf /var/lib/apt/lists/* && \
  curl -L https://github.com/sstephenson/ruby-build/archive/v20180329.tar.gz | tar -zxvf - -C /tmp/ && \
  cd /tmp/ruby-build-* && ./install.sh && cd / && \
  ruby-build -v 2.5.1 /usr/local && rm -rfv /tmp/ruby-build-*

RUN apt-get update && gem install bundler

# Insall nodejs
RUN curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -; \
  apt-get install -y nodejs

# Install yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list

RUN apt-get update && sudo apt-get install yarn

RUN usermod -aG docker,staff jenkins

RUN mkdir -p /var/www/jenkins; \
  chown -R jenkins:jenkins /var/www/jenkins

USER jenkins

# Install Jenkins plugins
RUN install-plugins.sh \
  blueocean \
  docker-workflow \
  locale \
  workflow-aggregator \
  pipeline-stage-view \
  git \
  cloudbees-bitbucket-branch-source \
  github-organization-folder

VOLUME [ "/var/www/jenkins" ]
