FROM java:7-jre

VOLUME ["/usr/share/elasticsearch/config", "/usr/share/elasticsearch/data"]

RUN apt-key adv --keyserver pool.sks-keyservers.net --recv-keys 46095ACC8548582C1A2699A9D27D666CD88E42B4

ENV ELASTICSEARCH_VERSION 1.4.4

RUN echo "deb http://packages.elasticsearch.org/elasticsearch/${ELASTICSEARCH_VERSION%.*}/debian stable main" > /etc/apt/sources.list.d/elasticsearch.list

RUN apt-get update \
	&& apt-get install elasticsearch=$ELASTICSEARCH_VERSION \
	&& rm -rf /var/lib/apt/lists/*

ENV PATH /usr/share/elasticsearch/bin:$PATH
COPY config /usr/share/elasticsearch/config

RUN /usr/share/elasticsearch/bin/plugin -install elasticsearch/elasticsearch-cloud-aws/2.4.1 \
    && /usr/share/elasticsearch/bin/plugin -install mobz/elasticsearch-head \
    && /usr/share/elasticsearch/bin/plugin -install lukas-vlcek/bigdesk \
    && /usr/share/elasticsearch/bin/plugin -install elasticsearch/elasticsearch-analysis-icu/2.4.2

EXPOSE 9200 9300

CMD ["elasticsearch"]
