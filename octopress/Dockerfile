FROM ubuntu:14.04

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update; \
  apt-get -q -y upgrade

RUN apt-get -q -y install git curl; \
  apt-get clean

# SSH set up to access GitHub repo
RUN mkdir -p /root/.ssh
ADD ssh/ /root/.ssh/
RUN chmod 600 /root/.ssh/*
RUN git clone -b source git@github.com:fabiocognigni/fabiocognigni.github.io.git /opt/octopress

# HTTP access - with usrname and pwd in line (not recommended)
# RUN git clone -b source https://my-usrname:my-pwd@github.com/fabiocognigni/fabiocognigni.github.io.git /opt/octopress

# Added BY ME to fix GPG signature verification failure
RUN gpg --keyserver hkp://keys.gnupg.net --recv-keys D39DC0E3

RUN curl -L https://get.rvm.io | bash -s stable --ruby

ENV HOME /root

RUN echo "source /usr/local/rvm/scripts/rvm" >> /root/.bashrc; 

#RUN /bin/bash -l -c "source /usr/local/rvm/scripts/rvm; \
#  rvm install 2.1.4; \
#  rvm use 2.1.4; \
#  rvm rubygems latest; \
#  cd /opt/octopress; \
#  gem install bundler; \
#  bundle install; \
#  rake install" 

# same as abobe but with no rake install (themes are already installed)
RUN /bin/bash -l -c "source /usr/local/rvm/scripts/rvm; \
  rvm install 2.1.4; \
  rvm use 2.1.4; \
  rvm rubygems latest; \
  cd /opt/octopress; \
  gem install bundler; \
  bundle install; \
  gem install rake --version=0.9.2.2"

RUN echo "rvm use 2.1.4" >> /root/.bashrc

# make sure we're working in UTF8
ENV LC_ALL en_US.utf8

WORKDIR /opt/octopress

EXPOSE 4000

CMD /bin/bash -l -c "rake preview"
# ENTRYPOINT ["rake", "preview"]

# Run Octopress
# CMD ["rake", "preview"]
# CMD /usr/local/rvm/gems/ruby-2.1.4/bin/rake preview