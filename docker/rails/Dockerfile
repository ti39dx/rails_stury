FROM centos:centos7

ENV LANG=ja_JP.UTF-8
RUN localedef -f UTF-8 -i ja_JP ja_JP.UTF-8

RUN cp -p /usr/share/zoneinfo/Japan /etc/localtime \
&&  echo 'ZONE="Asia/Tokyo"' > /etc/sysconfig/clock

RUN yum install -y \
    epel-release \
    openssl-devel \
    readline-devel\
    zlib-devel \
    less \
    wget \
    curl \
    git \
    dtach \
    vim \
    hash-slinger \
    bzip2 \
    tar \
    sqlite-devel \
    gcc-c++ \
    make \
    sox \
&&  yum groupinstall "Development Tools" -y \
&&  yum clean all

RUN curl --silent --location https://rpm.nodesource.com/setup_10.x | bash - \
    && yum -y install nodejs \
    && npm -g up \
    && npm install -g forever \
    && npm install -g hotnode \
    && npm install -g @vue/cli

RUN yum -y update && \
    yum -y install epel-release && \
    yum -y install git make autoconf curl wget && \
    yum -y install gcc-c++ glibc-headers openssl-devel readline libyaml-devel readline-devel zlib zlib-devel sqlite-devel bzip2 && \
    yum clean all

RUN git clone git://github.com/rbenv/rbenv.git /usr/local/rbenv \
&&  git clone git://github.com/rbenv/ruby-build.git /usr/local/rbenv/plugins/ruby-build \
&&  git clone git://github.com/jf/rbenv-gemset.git /usr/local/rbenv/plugins/rbenv-gemset \
&&  /usr/local/rbenv/plugins/ruby-build/install.sh
ENV PATH /usr/local/rbenv/bin:$PATH
ENV RBENV_ROOT /usr/local/rbenv

RUN echo 'export RBENV_ROOT=/usr/local/rbenv' >> /etc/profile.d/rbenv.sh \
&&  echo 'export PATH=/usr/local/rbenv/bin:$PATH' >> /etc/profile.d/rbenv.sh \
&&  echo 'eval "$(rbenv init -)"' >> /etc/profile.d/rbenv.sh

RUN echo 'export RBENV_ROOT=/usr/local/rbenv' >> /root/.bashrc \
&&  echo 'export PATH=/usr/local/rbenv/bin:$PATH' >> /root/.bashrc \
&&  echo 'eval "$(rbenv init -)"' >> /root/.bashrc

ENV CONFIGURE_OPTS --disable-install-doc
ENV PATH /usr/local/rbenv/bin:/usr/local/rbenv/shims:$PATH

ENV RBENV_VERSION 2.5.1

RUN eval "$(rbenv init -)"; rbenv install $RBENV_VERSION \
&&  eval "$(rbenv init -)"; rbenv global $RBENV_VERSION \
&&  eval "$(rbenv init -)"; gem update --system \
&&  eval "$(rbenv init -)"; gem install bundler -f \
&&  rm -rf /tmp/*

RUN eval "$(rbenv init -)"; gem install rspec --no-ri --no-rdoc
RUN eval "$(rbenv init -)"; gem install rails --no-ri --no-rdoc

EXPOSE 3000

CMD ["bash"]
