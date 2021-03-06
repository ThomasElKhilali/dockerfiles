# goalign
# https://github.com/fredericlemoine/goalign/
# v0.2.6c

# base image: Ubuntu
FROM ubuntu:16.04

# File Author / Maintainer
MAINTAINER Frederic Lemoine <frederic.lemoine@pasteur.fr>

ENV PATH=/usr/local/go/bin:/gopath/bin/:$PATH
ENV GOPATH=/gopath

RUN apt-get update --fix-missing \
    && apt-get install -y wget git \
    && cd /usr/local \
    && wget --no-check-certificate https://storage.googleapis.com/golang/go1.9.2.linux-amd64.tar.gz \
    && tar -C /usr/local -xzf go1.9.2.linux-amd64.tar.gz \
    && rm -f go1.9.2.linux-amd64.tar.gz \
    && mkdir -p /gopath/ \
    && go get -u github.com/golang/dep/cmd/dep \
    && mkdir -p /gopath/src/github.com/fredericlemoine/ \
    && cd /gopath/src/github.com/fredericlemoine/ \
    && wget -O goalign-0.2.6c.tar.gz https://github.com/fredericlemoine/goalign/archive/v0.2.6c.tar.gz \
    && tar -xzvf goalign-0.2.6c.tar.gz \
    && mv goalign-0.2.6c goalign \
    && rm -rf goalign-0.2.6c.tar.gz \
    && cd /gopath/src/github.com/fredericlemoine/goalign \
    && dep ensure \
    && go build -o goalign -ldflags "-X github.com/fredericlemoine/goalign/cmd.Version=v0.2.6c" github.com/fredericlemoine/goalign \
    && go test github.com/fredericlemoine/goalign/... \
    && mv goalign /usr/local/bin/ \
    && bash ./test.sh \
    && cd /usr/local \
    && rm -rf /gopath /usr/local/go \
    && apt-get remove -y wget git \
    && apt-get autoremove -y \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && mkdir /pasteur

ENTRYPOINT ["/usr/local/bin/goalign"]
