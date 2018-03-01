FROM centos:7

# author
MAINTAINER ken0nek

# metadata
LABEL version="1.0"
LABEL description="vips with dzsave"

ARG VIPS_VERSION_MAJOR_MINOR=8.5
ARG VIPS_VERSION_PATCH=9

ARG OPENSLIDE_VERSION_MAJOR_MINOR=3.4
ARG OPENSLIDE_VERSION_PATCH=1

# yum
RUN yum groupinstall -y "Development Tools"

RUN yum install -y tar \
               curl \
               libpng-devel \
               libjpeg-devel \
               libxml2-devel \
               zlib-devel \
               openjpeg-libs \
               openjpeg-devel \
               libtiff-devel \
               libtiff-tools \
               gdk-pixbuf2-devel \
               sqlite-devel \
               cairo-devel \
               glib2-develi \
               ImageMagick \
               ImageMagick-devel \
               which

ENV PKG_CONFIG_PATH $PKG_CONFIG_PATH:/usr/local/lib/pkgconfig:/usr/lib/pkgconfig

# libgsf-1
RUN curl -O http://ftp.acc.umu.se/pub/gnome/sources/libgsf/1.14/libgsf-1.14.42.tar.xz && \
    tar xfv libgsf-1.14.42.tar.xz && \
    cd libgsf-1.14.42 && \
    ./configure --disable-static --prefix=/usr && \
    make && \
    make install && \
    cd .. && \
    rm -rf libgsf-1.14.42 && \
    rm libgsf-1.14.42.tar.xz && \
    echo $PKG_CONFIG_PATH && \
    pkg-config libgsf-1 --modversion

# openslide
RUN curl -L -O https://github.com/openslide/openslide/releases/download/v${OPENSLIDE_VERSION_MAJOR_MINOR}.${OPENSLIDE_VERSION_PATCH}/openslide-${OPENSLIDE_VERSION_MAJOR_MINOR}.${OPENSLIDE_VERSION_PATCH}.tar.gz && \
    tar xzfv openslide-${OPENSLIDE_VERSION_MAJOR_MINOR}.${OPENSLIDE_VERSION_PATCH}.tar.gz && \
    cd openslide-${OPENSLIDE_VERSION_MAJOR_MINOR}.${OPENSLIDE_VERSION_PATCH} && \
    ./configure --prefix=/usr && \
    make && \
    make install && \
    cd .. && \
    rm -rf openslide-${OPENSLIDE_VERSION_MAJOR_MINOR}.${OPENSLIDE_VERSION_PATCH} && \
    rm openslide-${OPENSLIDE_VERSION_MAJOR_MINOR}.${OPENSLIDE_VERSION_PATCH}.tar.gz && \
    ldconfig && \
    pkg-config openslide --modversion

# vips
RUN curl -L -O https://github.com/jcupitt/libvips/releases/download/v${VIPS_VERSION_MAJOR_MINOR}.${VIPS_VERSION_PATCH}/vips-${VIPS_VERSION_MAJOR_MINOR}.${VIPS_VERSION_PATCH}.tar.gz && \
    tar xzfv vips-${VIPS_VERSION_MAJOR_MINOR}.${VIPS_VERSION_PATCH}.tar.gz && \
    cd vips-${VIPS_VERSION_MAJOR_MINOR}.${VIPS_VERSION_PATCH} && \
    ./configure --disable-debug --disable-docs --disable-static --disable-introspection --enable-cxx=yes --without-python --without-orc --without-fftw --prefix=/usr && \
    make && \
    make install && \
    cd .. && \
    rm -rf vips-${VIPS_VERSION_MAJOR_MINOR}.${VIPS_VERSION_PATCH} && \
    rm vips-${VIPS_VERSION_MAJOR_MINOR}.${VIPS_VERSION_PATCH}.tar.gz && \
    ldconfig

