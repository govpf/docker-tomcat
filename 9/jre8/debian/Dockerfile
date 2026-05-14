FROM govpf/openjdk:8-jre-debian

RUN apt-get update && \
    apt-get install -yq --no-install-recommends wget curl pwgen ca-certificates && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

ENV TOMCAT_MAJOR_VERSION 9
ENV TOMCAT_MINOR_VERSION 9.0.8
ENV JDBC_POSTGRESQL_VERSION 42.2.10
ENV CATALINA_HOME /tomcat

# INSTALL TOMCAT
RUN wget -q https://archive.apache.org/dist/tomcat/tomcat-${TOMCAT_MAJOR_VERSION}/v${TOMCAT_MINOR_VERSION}/bin/apache-tomcat-${TOMCAT_MINOR_VERSION}.tar.gz && \
    wget -qO- https://archive.apache.org/dist/tomcat/tomcat-${TOMCAT_MAJOR_VERSION}/v${TOMCAT_MINOR_VERSION}/bin/apache-tomcat-${TOMCAT_MINOR_VERSION}.tar.gz.sha512 | sha512sum -c - && \
    tar zxf apache-tomcat-*.tar.gz && \
    rm apache-tomcat-*.tar.gz && \
    mv apache-tomcat* tomcat && \
    cd tomcat/lib && \
    wget -q https://jdbc.postgresql.org/download/postgresql-${JDBC_POSTGRESQL_VERSION}.jar && \
    mv postgresql-${JDBC_POSTGRESQL_VERSION}.jar postgresql.jar && \
    chmod 640 postgresql.jar

# Suppression de l'app par défaut
RUN rm -rf /tomcat/webapps/*

ADD run.sh /run.sh
RUN chmod +x /*.sh

EXPOSE 8080
CMD ["/run.sh"]