# Copyright 2015-2022 Yelp Inc.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

ARG DOCKER_REGISTRY=docker-dev.yelpcorp.com/
FROM ${DOCKER_REGISTRY}ubuntu:focal

ARG PIP_INDEX_URL=https://pypi.yelpcorp.com/focal/simple
ENV PIP_INDEX_URL=$PIP_INDEX_URL
RUN rm /etc/dpkg/dpkg.cfg.d/excludes
RUN apt-get update && apt-get install -yq gnupg2

RUN apt-get update > /dev/null && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        build-essential \
        debhelper \
        gdebi-core \
        git \
        libffi-dev \
        libgpgme11 \
        libgpgme-dev \
        libssl-dev \
        libyaml-dev \
        python3-dev \
        python3-pip \
        python3-distutils-extra \
        # py2 used for just dh-virtualenv \
        python \
        tox \
        wget \
        sphinx-rtd-theme-common \
        zsh > /dev/null \
    && rm -rf /var/lib/apt/lists/*

RUN python3.8 -m pip install --upgrade pip==20.0.2
RUN pip3 install virtualenv==16.0.0
RUN cd /tmp && \
    wget http://mirrors.kernel.org/ubuntu/pool/universe/d/dh-virtualenv/dh-virtualenv_1.0-1_all.deb && \
    gdebi -n dh-virtualenv*.deb && \
    rm dh-virtualenv_*.deb

ADD mesos-slave-secret /etc/mesos-slave-secret

WORKDIR /work
