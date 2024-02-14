ARG SHARE_TAG
FROM quay.io/alfresco/alfresco-share:${SHARE_TAG}

USER root
ARG TOMCAT_DIR=/usr/local/tomcat
ARG RESOURCE_PATH=resources

RUN sed -i 's|shared.loader=\${catalina.base}\/shared\/classes|shared.loader="\${catalina.base}\/shared\/classes","\${catalina.base}\/shared\/lib"|g' ${TOMCAT_DIR}/conf/catalina.properties

COPY $RESOURCE_PATH/*.amp ${TOMCAT_DIR}/amps_share

RUN java -jar ${TOMCAT_DIR}/alfresco-mmt/alfresco-mmt*.jar install \
              ${TOMCAT_DIR}/amps_share ${TOMCAT_DIR}/webapps/share -directory -nobackup -force