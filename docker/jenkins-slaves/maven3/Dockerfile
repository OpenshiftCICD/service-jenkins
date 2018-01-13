#FROM slave-oracle-jdk8:8u151
FROM openshift/jenkins-slave-base-centos7

ARG VERSION

# Environment variables
ENV MAVEN_HOME=/maven-${VERSION} \
    MVN_HOME=/maven-${VERSION} \
    M2_HOME=${HOME}/.m2 \
    BASH_ENV=/usr/local/bin/scl_enable \
    ENV=/usr/local/bin/scl_enable \
    PROMPT_COMMAND=". /usr/local/bin/scl_enable"
ENV PATH="${PATH}:${MAVEN_HOME}/bin"

USER root

# Add default settigns.xml
COPY contrib/settings.xml ${M2_HOME}/settings.xml
COPY contrib/configure-slave /usr/local/bin/configure-slave
COPY contrib/configure-slave /usr/local/bin/scl_enable

# Make directories
RUN mkdir -p ${MAVEN_HOME} \
    && mkdir -p ${M2_HOME}/repository \
    && yum install -y centos-release-scl-rh \
    && curl -L http://mirror.klaus-uwe.me/apache/maven/maven-3/${VERSION}/binaries/apache-maven-${VERSION}-bin.tar.gz \
      | tar xz --strip-components=1 -C ${MAVEN_HOME} \
    && chmod -R g+rwX ${MAVEN_HOME} \
    && yum clean all -y \
    && yum autoremove -y \
    && rm -rf /var/cache/yum

USER 1001
