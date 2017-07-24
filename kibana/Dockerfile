FROM openjdk:8-jre-slim

ENV KIBANA_HOME=/kibana

RUN apt-get update && \
    apt-get install -y curl && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    curl -L https://artifacts.elastic.co/downloads/kibana/kibana-5.5.0-linux-x86_64.tar.gz | tar xzf - && \
    apt-get remove -y curl && \
    mv kibana-5.5.0-linux-x86_64 $KIBANA_HOME

COPY kibana.yml $KIBANA_HOME/config/kibana.yml

WORKDIR $KIBANA_HOME

EXPOSE 5601

CMD ["./bin/kibana"]
