FROM python:3.6

LABEL maintainer="renault@karudev.fr"

# Install Ubuntu packages
RUN apt-get update
RUN apt-get install alien dpkg-dev debhelper build-essential libaio1 --assume-yes

# Install VIM
RUN apt-get install libncurses5-dev libgnome2-dev libgnomeui-dev \
    libgtk2.0-dev libatk1.0-dev libbonoboui2-dev \
    libcairo2-dev libx11-dev libxpm-dev libxt-dev python-dev \
    python3-dev ruby-dev lua5.1 lua5.1-dev libperl-dev git -y

RUN cd ~ && git clone https://github.com/vim/vim.git
RUN cd ~/vim && ./configure --with-features=huge \
            --enable-multibyte \
            --enable-rubyinterp=yes \
            --enable-pythoninterp=yes \
            --with-python-config-dir=/usr/lib/python2.7/config \
            --enable-python3interp=yes \
            --with-python3-config-dir=/usr/lib/python3.4/config-3.4m-x86_64-linux-gnu \
            --enable-perlinterp=yes \
            --enable-luainterp=yes \
            --enable-gui=gtk2 --enable-cscope --prefix=/usr \
    make VIMRUNTIMEDIR=/usr/share/vim/vim80
RUN cd ~/vim && make install


# Install Oracle
ADD oracle-instantclient12.1-basic-12.1.0.2.0-1.x86_64.rpm .
ADD oracle-instantclient12.1-sqlplus-12.1.0.2.0-1.x86_64.rpm .
ADD oracle-instantclient12.1-devel-12.1.0.2.0-1.x86_64.rpm .
ADD oracle.conf /etc/ld.so.conf.d/oracle.conf
ADD oracle.sh /etc/profile.d/oracle.sh
RUN chmod +x /etc/ld.so.conf.d/oracle.conf
RUN chmod +x /etc/profile.d/oracle.sh

RUN alien -i oracle-instantclient12.1-basic-12.1.0.2.0-1.x86_64.rpm
RUN alien -i oracle-instantclient12.1-sqlplus-12.1.0.2.0-1.x86_64.rpm
RUN alien -i oracle-instantclient12.1-devel-12.1.0.2.0-1.x86_64.rpm

RUN /etc/profile.d/oracle.sh
RUN ldconfig

# Install python app
ADD requirements.txt /code/
WORKDIR /code
RUN pip install -r requirements.txt

