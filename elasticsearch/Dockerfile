FROM openjdk:8-jre-slim

ARG user=elasticsearch
ARG group=elasticsearch
ARG groupid=1001

RUN groupadd -g ${groupid} ${group} && \
    useradd -g ${group} ${user}

ENV ES_VERSION=5.5.0
ENV ES_HOME="/elasticsearch"
#ENV CLUSTER_NAME=default_cluster
#ENV NODE_NAME=default_node

RUN apt-get update && \
    apt-get install -y curl && \
    curl -L https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-$ES_VERSION.tar.gz | tar xzf - && \
    mv elasticsearch-$ES_VERSION $ES_HOME && \
    mkdir $ES_HOME/data && \
    $ES_HOME/bin/elasticsearch-plugin install analysis-kuromoji

# Add config file
COPY elasticsearch.yml $ES_HOME/config/elasticsearch.yml

RUN chown -R ${user}:${group} $ES_HOME && \
    apt-get remove -y curl && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

USER ${user}

VOLUME $ES_HOME/data

WORKDIR $ES_HOME

EXPOSE 9300 9200

ENTRYPOINT ["./bin/elasticsearch"]
