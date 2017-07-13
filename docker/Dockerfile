FROM python:3.6

LABEL maintainer="renault@karudev.fr"

# Install Ubuntu packages 
RUN apt-get update
RUN apt-get install alien dpkg-dev debhelper build-essential libaio1 --assume-yes

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

