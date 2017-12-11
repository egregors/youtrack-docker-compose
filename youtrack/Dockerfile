FROM java:8-jre
LABEL maintainer=kabanov.mike@gmail.com

RUN mkdir -p /opt/youtrack/data /opt/youtrack/backup /opt/youtrack/bin
WORKDIR /opt/youtrack

ARG YOUTRACK_VERSION

RUN wget \
 https://download.jetbrains.com/charisma/youtrack-$YOUTRACK_VERSION.jar \
 -O /opt/youtrack/bin/youtrack.jar

EXPOSE 8001/tcp

VOLUME ["/opt/youtrack/data/", "/opt/youtrack/backup/"]
CMD ["java", "-Xmx1g", "-XX:MaxMetaspaceSize=250m", "-Duser.home=/opt/youtrack", "-Ddatabase.location=/opt/youtrack/data", "-Ddatabase.backup.location=/opt/youtrack/backup", "-Djavax.net.ssl.trustStore=/etc/ssl/certs/java/cacerts", "-Djavax.net.ssl.trustStorePassword=changeit", "-Djetbrains.youtrack.disableBrowser=true", "-Djetbrains.youtrack.enableGuest=false", "-Djava.awt.headless=true", "-Djetbrains.youtrack.disableCheckForUpdate=true", "-Djava.security.egd=/dev/urandom", "-jar", "/opt/youtrack/bin/youtrack.jar", "8001"]
