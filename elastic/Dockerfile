FROM java:8-jre

RUN apt-get update
RUN apt-get install -y wget
RUN apt-get install -y sysstat


ENV ES_VERSION 2.3.3


WORKDIR /opt

RUN useradd -g staff -ms /bin/bash elastic

RUN wget -O- https://download.elasticsearch.org/elasticsearch/release/org/elasticsearch/distribution/tar/elasticsearch/$ES_VERSION/elasticsearch-$ES_VERSION.tar.gz  | tar xfz -
RUN mv /opt/elasticsearch-$ES_VERSION /opt/elasticsearch

RUN /opt/elasticsearch/bin/plugin install license
RUN /opt/elasticsearch/bin/plugin install marvel-agent
RUN /opt/elasticsearch/bin/plugin install graph
RUN /opt/elasticsearch/bin/plugin install discovery-multicast

VOLUME /data
VOLUME /config
VOLUME /logs

ENV ES_JAVA_OPTS -Des.path.conf=/config

USER elastic
WORKDIR /opt/elasticsearch/bin

CMD ["/opt/elasticsearch/bin/elasticsearch"]
