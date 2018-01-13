FROM openshift/jenkins-slave-base-centos7

MAINTAINER Thomas Herzog <herzog.thomas81@gmail.com>

# Should be Build arguments but openshift builds does not provide yet (3.5)
ARG JDK_ARTIFACT_ID
ARG JDK_VERSION

ENV JAVA_HOME="/opt/oracle-jdk8"
ENV PATH="${PATH}:${JAVA_HOME}/bin"

# Bad approach because will be in layer. Newer version of openshift allow using of buildArgs
ADD nexus-user /nexus-user
ADD nexus-password /nexus-password
ADD nexus-url /nexus-url

# Remove openjdk
RUN yum install -y centos-release-scl-rh \
    && mkdir -p ${JAVA_HOME} \
    && curl -u $(cat /nexus-user):$(cat /nexus-password) -L $(cat /nexus-url)/com/oracle/${JDK_ARTIFACT_ID}/${JDK_VERSION}/${JDK_ARTIFACT_ID}-${JDK_VERSION}.tar.gz \
    | tar xz --strip-components=1 -C ${JAVA_HOME} \
    && chown -R 1001:1001 ${JAVA_HOME} \
    && chmod -R 777 ${JAVA_HOME} \
    && yum clean all -y \
    && yum autoremove -y \
    && rm -rf /var/cache/yum \
    && rm -rf /nexus-*
