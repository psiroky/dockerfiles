# heavily based on https://github.com/goldmann/dockerfiles/blob/master/awestruct/Dockerfile
# we need to use a 'jenkins' user to make this easily work with
# https://wiki.jenkins-ci.org/display/JENKINS/CloudBees+Docker+Custom+Build+Environment+Plugin
FROM fedora:23

MAINTAINER "Petr Široký <psiroky@redhat.com>"

RUN dnf -y update && dnf clean all
RUN dnf -y install \
  autoconf \
  automake \
  bison \
  bzip2 \
  gcc-c++ \
  git \
  glibc-devel \
  glibc-headers \
  libffi-devel \
  libtool \
  libxml2-devel \
  libxslt-devel \
  libyaml-devel \
  make \
  openssl-devel \
  patch \
  patch \
  readline-devel \
  sqlite-devel \
  which \
  zlib-devel \
  procps-ng \
&& dnf clean all

RUN useradd -m jenkins -u 1000

USER jenkins
WORKDIR /home/jenkins

ENV HOME /home/jenkins
ENV RUBY_VERSION 2.3.1
ENV AWESTRUCT_VERSION 0.5.7
ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8

RUN gpg2 --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
RUN curl -sSL https://get.rvm.io | bash -s stable --ruby=$RUBY_VERSION
 
RUN bash -l -c "rvm use $RUBY_VERSION"
RUN bash -l -c "rvm cleanup all"
RUN bash -l -c "gem install awestruct -v $AWESTRUCT_VERSION --no-rdoc --no-ri"
RUN bash -l -c "gem install bundler"

EXPOSE 4242

CMD ["bash", "--login"]
