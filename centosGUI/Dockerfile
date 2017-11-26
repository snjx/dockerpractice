FROM centos

# yum install
RUN yum -y update

# GUI関係のyumインストール
RUN yum -y groupinstall "Server with GUI"
RUN yum -y install alacarte

# 日本語環境
#RUN timedatectl set-timezone Asia/Tokyo
#RUN localectl set-locale LANG=ja_JP.UTF-8
#RUN systemctl set-default graphical.target

# 開発関係のyumインストール
RUN yum -y groupinstall 'Development Tools'
RUN yum -y install gcc git rsync bzip2 tar openssl openssl-devel readline-devel  zlib-devel libffi-devel gdbm-devel tk tk-devel tcl tcl-devel patch gcc-c++ which sqlite-devel wget openssh-server file
RUN yum -y install mariadb mariadb-server mysql-devel
RUN yum -y install ImageMagick ImageMagick-devel ipa-pgothic-fonts
RUN yum -y install subversion

# rbenvのインストール
RUN git clone https://github.com/sstephenson/rbenv.git /root/.rbenv
RUN git clone https://github.com/sstephenson/ruby-build.git /root/.rbenv/plugins/ruby-build
RUN ./root/.rbenv/plugins/ruby-build/install.sh
ENV PATH /root/.rbenv/shims:/root/.rbenv/bin:$PATH
RUN echo 'export PATH=/root/.rbenv/shims:/root/.rbenv/bin:$PATH' >> /root/.bashrc
RUN echo 'eval "$(rbenv init -)"' >> /root/.bashrc
RUN source /root/.bashrc

# rubyのインストール(2.4.2)
ENV CONFIGURE_OPTS --disable-install-doc
RUN rbenv install 2.4.2
RUN rbenv global 2.4.2
RUN rbenv rehash
RUN rbenv exec gem install bundler
RUN rbenv rehash
# bundlerのインストール
RUN gem install bundler --no-rdoc --no-ri

# Javaインストール
RUN yum -y install java-1.8.0-openjdk
RUN yum -y install java-1.8.0-openjdk

# centosの起動
CMD /sbin/init
