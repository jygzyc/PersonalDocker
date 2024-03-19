FROM ubuntu:22.04

# ndk env
ENV ANDROID_NDK_HOME /opt/android-ndk
ARG android_ndk_version 
ENV ANDROID_NDK_VERSION ${android_ndk_version}
ENV XMAKE_ROOT y

# ------------------------------------------------------
# --- Install required tools

# Modify the sources.list for improving download speed 
RUN sed -i 's@//.*archive.ubuntu.com@//mirrors.ustc.edu.cn@g' /etc/apt/sources.list

ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update -qq && apt-get clean
RUN apt-get install -y \
    build-essential \
    curl \
    git \
    make \
    unzip \
    wget \
    software-properties-common

RUN add-apt-repository ppa:xmake-io/xmake
RUN apt-get update -qq && apt-get clean
RUN apt-get install xmake

# ------------------------------------------------------
# --- Android NDK
# download
RUN mkdir /opt/android-ndk-tmp && \
    cd /opt/android-ndk-tmp && \
    wget -t 3 -c https://dl.google.com/android/repository/android-ndk-${ANDROID_NDK_VERSION}-linux.zip && \
# uncompress
    unzip -q android-ndk-${ANDROID_NDK_VERSION}-linux.zip && \
# move to its final location
    mv ./android-ndk-${ANDROID_NDK_VERSION} ${ANDROID_NDK_HOME} && \
# remove temp dir
    cd ${ANDROID_NDK_HOME} && \
    rm -rf /opt/android-ndk-tmp
# add to PATH
ENV PATH ${PATH}:${ANDROID_NDK_HOME}

RUN xmake g --ndk=${ANDROID_NDK_HOME}

# ------------------------------------------------------
# Workdir config
VOLUME /project
ENV WORKDIR /project 
WORKDIR $WORKDIR


