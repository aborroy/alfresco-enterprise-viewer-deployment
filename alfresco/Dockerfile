ARG ALFRESCO_TAG
FROM quay.io/alfresco/alfresco-content-repository:${ALFRESCO_TAG}

ARG USERNAME=alfresco
ARG RESOURCE_PATH=resources
ARG TOMCAT_DIR=/usr/local/tomcat

USER root

RUN mkdir ${TOMCAT_DIR}/shared/classes/alfresco/module \
          ${TOMCAT_DIR}/shared/classes/alfresco/module/com.tsgrp.opencontent \
          ${TOMCAT_DIR}/shared/lib

COPY ${RESOURCE_PATH}/opencontent-override-placeholders.properties \
        ${TOMCAT_DIR}/shared/classes/alfresco/module/com.tsgrp.opencontent/
COPY ${RESOURCE_PATH}/opencontent-override-config.xml \
        ${TOMCAT_DIR}/shared/classes/alfresco/module/com.tsgrp.opencontent/
COPY ${RESOURCE_PATH}/opencontent-override-module-context.xml \
        ${TOMCAT_DIR}/shared/classes/alfresco/module/com.tsgrp.opencontent/

COPY ${RESOURCE_PATH}/*.amp ${TOMCAT_DIR}/amps
RUN java -jar ${TOMCAT_DIR}/alfresco-mmt/alfresco-mmt*.jar install \
              ${TOMCAT_DIR}/amps ${TOMCAT_DIR}/webapps/alfresco -directory -nobackup -force

COPY ${RESOURCE_PATH}/OpenAnnotate.war ${TOMCAT_DIR}/webapps/
COPY ${RESOURCE_PATH}/oat.war ${TOMCAT_DIR}/webapps/

# install truetype arial fonts
RUN yum install -y unzip
RUN mkdir /usr/local/fonts
COPY ${RESOURCE_PATH}/ttf.zip /usr/share/fonts
RUN unzip /usr/share/fonts/ttf.zip -d /usr/share/fonts
RUN fc-cache -v /usr/share/fonts/ && fc-cache-64 -v /usr/share/fonts/

# install pdfium
RUN mkdir /opt/pdfium
COPY ${RESOURCE_PATH}/pdfium.tar.gz /
RUN tar -zxvf /pdfium.tar.gz -C /opt/pdfium

RUN chown -R ${USERNAME} $TOMCAT_DIR

USER ${USERNAME}