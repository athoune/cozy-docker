FROM ubuntu:14.04

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get -y update && apt-get install -y couchdb pwgen curl

RUN useradd -M cozy \
 && useradd -M cozy-data-system

# Configure CouchDB.
RUN mkdir /etc/cozy \
 && chown -hR cozy /etc/cozy
RUN pwgen -1 > /etc/cozy/couchdb.login \
 && pwgen -1 >> /etc/cozy/couchdb.login \
 && chown cozy-data-system /etc/cozy/couchdb.login \
 && chmod 640 /etc/cozy/couchdb.login
#RUN mkdir /var/run/couchdb \
# && chown -hR couchdb /var/run/couchdb \
# && su - couchdb -c 'couchdb -b' \
# && sleep 5 \
# && while ! curl -s 127.0.0.1:5984; do sleep 5; done \
# && curl -s -X PUT 127.0.0.1:5984/_config/admins/$(head -n1 /etc/cozy/couchdb.login) -d "\"$(tail -n1 /etc/cozy/couchdb.login)\""

# Expose to the outside
RUN sed -e 's/^bind_address = .*$/bind_address = 0.0.0.0/' -i /etc/couchdb/default.ini

RUN mkdir -p /var/run/couchdb && chown couchdb /var/run/couchdb

EXPOSE 5984
#USER couchdb
VOLUME "/var/lib/couchdb"
#ENV HOME /usr/local/var/lib/couchdb
WORKDIR /var/lib/couchdb

CMD ["/usr/bin/couchdb"]
