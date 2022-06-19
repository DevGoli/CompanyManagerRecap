# Creates the minimum environment to package and run this Skyve application.
# Note that this uses an in-memory database and is only useful for demonstration/development.
FROM bizhubaustralia/skyve-wildfly-mysql:latest

ENV LANG en_US.UTF-8

USER root
RUN mkdir /content
RUN chown jboss:jboss /content

RUN mkdir -p /opt/skyve/addins/
RUN chown jboss:jboss /opt/skyve/addins/

USER jboss
ADD skyve-content-8.1.2.zip /opt/skyve/addins/skyve-content-8.1.2.zip
ADD companyManagerRecap.war /opt/jboss/wildfly/standalone/deployments/companyManagerRecap.war
ADD companyManagerRecap.json /opt/jboss/wildfly/standalone/deployments
RUN touch /opt/jboss/wildfly/standalone/deployments/companyManagerRecap.war.dodeploy

ENV SKYVE_CONTENT='/content/' \
    SKYVE_DATASTORE_DIALECT='org.skyve.impl.persistence.hibernate.dialect.MySQL8InnoDBSpatialDialect' \
    DATABASE_URL='companyManagerRecap_db' \
    SKYVE_SECURITY_DOMAIN_NAME='companyManagerRecap' \
    SKYVE_JNDI_NAME='companyManagerRecapDB'

ENTRYPOINT [ "entrypoint.sh" ]
CMD [ "/opt/jboss/wildfly/bin/standalone.sh", "-b", "0.0.0.0", "-Djava.locale.providers=COMPAT,CLDR" ]
