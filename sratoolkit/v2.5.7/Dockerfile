# sratoolkit
# https://www.ncbi.nlm.nih.gov/sra/docs/toolkitsoft/
# v2.5.7

FROM ubuntu:16.04

MAINTAINER Frederic Lemoine

RUN mkdir /pasteur

RUN apt-get update --fix-missing \
    && apt-get install -q -y wget \
    && wget -q http://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/2.5.7/sratoolkit.2.5.7-ubuntu64.tar.gz -O- | tar xz -C /opt/ \
    && mkdir /opt/sratoolkit \
    && ln -s /opt/sratoolkit.2.5.7-ubuntu64/bin/* /opt/sratoolkit/ \
    && groupadd -g 1001 srauser \
    && useradd -d /home/srauser -u 1001 -g 1001 -m -s /bin/bash srauser

USER srauser
ENV HOME /home/srauser

RUN cd /home/srauser/ \
    && wget http://download.asperasoft.com/download/sw/connect/3.6.2/aspera-connect-3.6.2.117442-linux-64.tar.gz \
    && tar -xzvf aspera-connect-3.6.2.117442-linux-64.tar.gz \
    && sh aspera-connect-3.6.2.117442-linux-64.sh \
    && rm aspera-connect-3.6.2.117442-linux-64.tar.gz


USER root
RUN apt-get remove -q -y wget \
    && apt-get autoremove -y \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

ENV HOME /root/
ENV PATH /bin/:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/home/srauser/.aspera/connect/bin/:/opt/sratoolkit
ENV ASCPKEY /home/srauser/.aspera/connect/etc/asperaweb_id_dsa.openssh

