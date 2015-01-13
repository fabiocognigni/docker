FROM ubuntu:14.04

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update; \
  apt-get -q -y upgrade

RUN apt-get -q -y install git curl; \
  apt-get clean

# TODO create ssh keys, copy into the docker img and set as deploy key in the GitHub repo
RUN git clone -b source git@github.com:fabiocognigni/fabiocognigni.github.io.git /opt/octopress
# RUN git clone -b source https://xxxxxx:yyyyyy@github.com/fabiocognigni/fabiocognigni.github.io.git /opt/octopress
# RUN git clone git://github.com/imathis/octopress.git /opt/octopress

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
# CMD /bin/bash -l -c "bundle exec rake preview"
# ENTRYPOINT ["rake", "preview"]

# Run Octopress
# CMD ["rake", "preview"]
# CMD /usr/local/rvm/gems/ruby-2.1.4/bin/rake preview