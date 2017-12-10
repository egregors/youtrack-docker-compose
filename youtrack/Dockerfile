FROM java:8-jre
LABEL maintainer=kabanov.mike@gmail.com

RUN mkdir -p /opt/youtrack/data /opt/youtrack/backup /opt/youtrack/bin
WORKDIR /opt/youtrack

RUN apt-get update && \
    apt-get install -y supervisor && \
    rm -rf /var/lib/apt/lists/*

ARG YOUTRACK_VERSION

RUN wget \
 https://download.jetbrains.com/charisma/youtrack-$YOUTRACK_VERSION.jar \
 -O /opt/youtrack/bin/youtrack.jar

ADD supervisor/youtrack.conf /etc/supervisor/conf.d/youtrack.conf

EXPOSE 8001/tcp

VOLUME ["/opt/youtrack/data/", "/opt/youtrack/backup/"]
CMD ["/usr/bin/supervisord","-n","-c","/etc/supervisor/supervisord.conf"]
