ARG IMAGE="manylinux2014"
ARG ARCH="x86_64"

FROM quay.io/pypa/${IMAGE}_${ARCH}:latest

LABEL maintainer.name="Luigi Pertoldi"
LABEL maintainer.email="gipert@pm.me"

USER root
WORKDIR /root

COPY . /root

RUN sed -i '/tsflags=nodocs/d' /etc/yum.conf && \
    yum -y update && \
    yum -y groupinstall "Development Tools" && \
    yum -y install $(cat packages) && \
    yum -y clean all && \
    ln -s /usr/include/boost169/boost /usr/include/boost && \
    dbus-uuidgen > /etc/machine-id

# manually installing OCCT because the version in the repos is too old
RUN mkdir -p OCCT/{src,build} && \
    wget -q -O- https://github.com/Open-Cascade-SAS/OCCT/archive/refs/tags/V7_6_0.tar.gz \
        | tar --strip-components 1 -C OCCT/src --strip=1 -x -z && \
    cd OCCT/build && \
    cmake -DCMAKE_INSTALL_PREFIX=/opt/opencascade ../src && \
    make -j$(nproc) && \
    make install && \
    cd ../ && \
    rm -rf OCCT

ENV PATH="/opt/opencascade/bin:$PATH" \
    LD_LIBRARY_PATH="/opt/opencascade/lib:$LD_LIBRARY_PATH"

# manually installing CGAL because the version in the repos is too old
RUN mkdir -p CGAL/{src,build} && \
    wget -q -O- https://github.com/CGAL/cgal/releases/download/v5.5.2/CGAL-5.5.2.tar.xz \
        | tar --strip-components 1 -C CGAL/src --strip=1 -x --xz && \
    cd CGAL/build && \
    cmake -DCMAKE_INSTALL_PREFIX=/opt/cgal -DCMAKE_BUILD_TYPE=Release ../src && \
    make -j$(nproc) && \
    make install && \
    cd ../ && \
    rm -rf CGAL

ENV PATH="/opt/cgal/bin:$PATH" \
    LD_LIBRARY_PATH="/opt/cgal/lib64:$LD_LIBRARY_PATH"
