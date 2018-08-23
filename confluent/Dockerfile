FROM gudaoxuri/java:latest
MAINTAINER gudaoxuri <i@sunisle.org>

# Setup env
ENV CONFLUENT_HOME /opt/confluent
ENV KAFKA_HOME /opt/confluent
ENV PATH $CONFLUENT_HOME/bin:$PATH
ENV KEEP false

RUN echo "export CONFLUENT_HOME=/opt/confluent" >> /etc/profile \
 && echo "export KAFKA_HOME=/opt/confluent" >> /etc/profile \
 && echo "export PATH=$CONFLUENT_HOME/bin:$PATH" >> /etc/profile

RUN wget -q -O - http://packages.confluent.io/archive/4.0/confluent-oss-4.0.0-2.11.tar.gz | tar -xzf - -C /opt/ \
 && mv /opt/confluent-4.0.0 /opt/confluent

COPY server.properties.template $CONFLUENT_HOME/etc/kafka/server.properties.template

COPY bootstrap_ssh.sh /bin/bootstrap_ssh.sh.sh
COPY bootstrap_keep.sh /bin/bootstrap_keep.sh
COPY bootstrap_confluent.sh /bin/bootstrap_confluent.sh
COPY bootstrap.sh /bin/bootstrap.sh

RUN chmod +x /bin/bootstrap.sh

EXPOSE 9092 8081 8082 8083

VOLUME ["$CONFLUENT_HOME/share/java"]

ENTRYPOINT /bin/bootstrap.sh $KEEP