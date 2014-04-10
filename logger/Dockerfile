FROM deis/base:latest
MAINTAINER Gabriel Monroy <gabriel@opdemand.com>

RUN apt-get update
RUN apt-get install -yq --force-yes openjdk-7-jre-headless

# Install logstash
RUN wget -q https://download.elasticsearch.org/logstash/logstash/logstash-1.4.0.tar.gz -O /opt/logstash-1.4.0.tar.gz
RUN cd /opt && tar -xzf logstash-1.4.0.tar.gz
RUN mv /opt/logstash-1.4.0 /opt/logstash

# create /var/log/deis for holding logs (access via bind mount)
RUN mkdir -p /var/log/deis

# install latest etcdctl including no-sync options
RUN wget -q https://s3-us-west-2.amazonaws.com/deis/etcdctl.no-sync -O /usr/local/bin/etcdctl
RUN chmod +x /usr/local/bin/etcdctl

# add the current build context to /app
ADD . /app

# prepare execution environment
WORKDIR /app
CMD ["/app/bin/boot"]
EXPOSE 514
