FROM quay.io/pypa/manylinux2014_x86_64:latest

USER root
WORKDIR /root

# configure system
COPY . /root
COPY puias.repo /etc/yum.repos.d/puias.repo

# cgal not in the official centos repos
RUN rpm --import http://springdale.math.ias.edu/data/puias/7/x86_64/os/RPM-GPG-KEY-puias
    # rpm --import http://springdale.math.ias.edu/data/puias/7/x86_64/os/RPM-GPG-KEY-springdale

RUN sed -i '/tsflags=nodocs/d' /etc/yum.conf && \
    yum -y update && \
    yum -y groupinstall "Development Tools" && \
    yum -y install $(cat packages) && \
    yum -y clean all && \
    dbus-uuidgen > /etc/machine-id

RUN patch -R /usr/include/opencascade/TDocStd_Application.hxx < patches/TDocStd_Application.patch
