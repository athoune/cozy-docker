FROM ubuntu:14.04

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y \
    python-dev \
    python-virtualenv \
    git \
    zlib1g-dev \
    libxslt1-dev \
    libxml2-dev

RUN useradd -M cozy
# Install Cozy Indexer.
RUN cd /usr/local/ \
 && git clone https://github.com/cozy/cozy-data-indexer.git

WORKDIR /usr/local/cozy-data-indexer

RUN virtualenv . && ./bin/pip install -r requirements/common.txt \
 && chown -R cozy:cozy .

USER cozy

# FIXME option to listen 0.0.0.0
EXPOSE 9102
CMD ["./bin/python", "server.py"]
