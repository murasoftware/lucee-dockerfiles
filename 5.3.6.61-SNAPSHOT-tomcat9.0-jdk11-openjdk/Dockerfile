FROM lucee/lucee:5.3.6.61-SNAPSHOT-tomcat9.0-jdk11-openjdk

ARG admin_pw=
ENV LUCEE_JAVA_OPTS "-Xms1024m -Xmx1024m"
ENV LUCEE_EXTENSIONS "17AB52DE-B300-A94B-E058BD978511E39E;name=S3;label=S3;version=0.9.4.122,7E673D15-D87C-41A6-8B5F1956528C605F;name=MySQL;label=MySQL;version=8.0.19,16FF9B13-C595-4FA7-B87DED467B7E61A0;Name=Memcached;version=3.0.2.29,99A4EF8D-F2FD-40C8-8FB8C2E67A4EEEB6;name=MSSQL;label=MS SQL Server;version=6.0.7728.100,D4EDFDBD-A9A3-E9AF-597322D767E0C949;Name=Oracle;version=12.1.0.2"

RUN mkdir /usr/local/tomcat/lucee-custom-lib

COPY catalina.properties server.xml /usr/local/tomcat/conf/

COPY rewrite.config /usr/local/tomcat/conf/Catalina/127.0.0.1/

RUN echo -n $admin_pw > /opt/lucee/server/lucee-server/context/password.txt

# https://github.com/lucee/lucee-dockerfiles/issues/61
RUN sed \
    -i 's~\(<Connector [^\>]*AJP/.*\)\( />\)~ \1 secretRequired="false" \2 ~' \
    '/usr/local/tomcat/conf/server.xml'

# lucee first time startup; explodes lucee and installs bundles/extensions (prewarms twice due to additional bundle downloads)
RUN /usr/local/tomcat/bin/prewarm.sh && /usr/local/tomcat/bin/prewarm.sh
