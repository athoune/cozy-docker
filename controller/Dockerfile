FROM ubuntu:14.04

RUN apt-get update && apt-get install -y \
    libssl-dev build-essential curl python

ENV NODE_VERSION 0.10.26
WORKDIR /tmp

RUN curl http://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION.tar.gz | tar xz \
 && cd node-v$NODE_VERSION \
 && ./configure \
 && CXX="g++ -Wno-unused-local-typedefs" make \
 && CXX="g++ -Wno-unused-local-typedefs" make install \
 && cd .. \
 && rm -rf /tmp/node-v*

RUN npm install -g npm

# Install CoffeeScript, Cozy Monitor and Cozy Controller via NPM.
RUN npm install -g \
  coffee-script \
  cozy-controller \
  cozy-monitor

EXPOSE 9104
ENV NODE_ENV production
CMD cozy-controller
