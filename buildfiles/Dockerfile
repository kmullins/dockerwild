FROM centos:7
MAINTAINER <Kevin Mullins kmmmullins@gmail.com>
#RUN yum update -y \
RUN yum -y install zip unzip wget    
ENV JAVA_HOME /usr/java/jdk1.8.0_151
ENV PATH "$PATH":/${JAVA_HOME}/bin:.:
ENV VERSION 10.1.0.Final
ENV INSTALL_DIR /opt
ENV WILDFLY_HOME ${INSTALL_DIR}/wildfly-${VERSION}
ENV DEPLOYMENT_DIR ${WILDFLY_HOME}/standalone/deployments/
ADD buildfiles/jdk-8u151-linux-x64.rpm /tmp
RUN yum install -y /tmp/jdk-8u151-linux-x64.rpm

RUN curl -O https://download.jboss.org/wildfly/${VERSION}/wildfly-${VERSION}.zip 
RUN unzip wildfly-${VERSION}.zip -d ${INSTALL_DIR} 
RUN rm wildfly-${VERSION}.zip 
#RUN rm ${WILDFLY_HOME}/bin/standalone.conf 
#    && chmod a+x ${WILDFLY_HOME}/bin/standalone.sh
#ADD standalone.conf ${WILDFLY_HOME}/bin/
ENTRYPOINT ${WILDFLY_HOME}/bin/standalone.sh -b=0.0.0.0
#EXPOSE 8080
# Insert here your war path. In this example these files are placed in a Maven project, so, the .war file is in target folder
#COPY target/docks.war ${DEPLOYMENT_DIR}

#COPY dsconfig /configtemp/dsconfig/

# Set the JBOSS_HOME env variable
ENV JBOSS_HOME /opt/wildfly


ENV DS_IP ${DS_IP:-i2b2-pg}
ENV DS_PORT ${DS_PORT:-5432}
ENV DS_TYPE ${DS_TYPE:-pg}
ENV DS_PASS ${DS_TYPE:-demouser}

ENV DS_CRC_IP ${DS_CRC_IP:-$DS_IP}
ENV DS_CRC_PORT ${DS_CRC_PORT:-$DS_PORT}
ENV DS_CRC_USER ${DS_CRC_USER:-i2b2demodata}
ENV DS_CRC_PASS ${DS_CRC_PASS:-$DS_PASS}

ENV DS_ONT_IP ${DS_CRC_IP:-$DS_IP}
ENV DS_ONT_PORT ${DS_CRC_PORT:-$DS_PORT}
ENV DS_ONT_USER ${DS_CRC_USER:-i2b2metadata}
ENV DS_ONT_PASS ${DS_CRC_PASS:-$DS_PASS}

ENV DS_PM_IP ${DS_CRC_IP:-$DS_IP}
ENV DS_PM_PORT ${DS_CRC_PORT:-$DS_PORT}
ENV DS_PM_USER ${DS_CRC_USER:-i2b2pm}
ENV DS_PM_PASS ${DS_CRC_PASS:-$DS_PASS}

ENV DS_WD_IP ${DS_CRC_IP:-$DS_IP}
ENV DS_WD_PORT ${DS_CRC_PORT:-$DS_PORT}
ENV DS_WD_USER ${DS_CRC_USER:-i2b2metadata}
ENV DS_WD_PASS ${DS_CRC_PASS:-$DS_PASS}

ENV DS_IM_IP ${DS_CRC_IP:-$DS_IP}
ENV DS_IM_PORT ${DS_CRC_PORT:-$DS_PORT}
ENV DS_IM_USER ${DS_CRC_USER:-i2b2imdata}
ENV DS_IM_PASS ${DS_CRC_PASS:-$DS_PASS}
COPY buildfiles/wfconfig ${WILDFLY_HOME}/standalone/configuration/
COPY buildfiles/prescript.sh ${WILDFLY_HOME}/bin/
RUN chmod +x ${WILDFLY_HOME}/bin/prescript.sh


#RUN ${WILDFLY_HOME}/bin/add-user.sh admin demoadmin --silent


# Expose the ports were interested in
EXPOSE 9090 

 CMD ["/bin/bash","-C","ps aux"]
