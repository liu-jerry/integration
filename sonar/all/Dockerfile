
# Pull base image.
FROM dockerfile/java:oracle-java8

MAINTAINER lzy7750015@gmail.com

ENV SONAR_JDBC_URL jdbc:mysql://mysql:3306/sonar?useUnicode=true&characterEncoding=utf8&rewriteBatchedStatements=true
ENV SONAR_USER sonar
ENV SONAR_PASSWORD sonar
ENV SONAR_LOG_LEVEL DEBUG
ENV	SONAR_WEB_CONTEXT /
ENV SONAR_HOME /usr/local/nexus

RUN \
  wget -O /tmp/sonar-latest.zip http://dist.sonar.codehaus.org/sonarqube-4.5.zip && \
  unzip /tmp/sonar-latest.zip -d /usr/local && \
  ln -s /usr/local/sonarqube-* /usr/local/sonar && \
  rm -rf /tmp/sonar-latest.zip && \
  sed -i 's/^#\(sonar.jdbc.url\)=\(jdbc:mysql:\S*\)/\1=${env:SONAR_JDBC_URL}\n#\1=\2/' /usr/local/sonar/conf/sonar.properties && \
  sed -i 's/^#\(sonar.jdbc.username\)=sonar/\1=${env:SONAR_USER}/' /usr/local/sonar/conf/sonar.properties && \
  sed -i 's/^#\(sonar.jdbc.password\)=sonar/\1=${env:SONAR_PASSWORD}/' /usr/local/sonar/conf/sonar.properties && \
  sed -i 's/^#\(sonar.web.context\)=/\1=${env:SONAR_WEB_CONTEXT}/' /usr/local/sonar/conf/sonar.properties

VOLUME ["/usr/local/sonar"]

WORKDIR /usr/local/sonar

CMD ["/usr/local/sonar/bin/linux-x86-64/sonar.sh","console"]

EXPOSE 9000

