#FROM slave-oracle-jdk8:8u151
FROM openshift/jenkins-slave-base-centos7

ARG VERSION

# Environment variables
ENV GRADLE_HOME=/gradle-${VERSION} \
    BASH_ENV=/usr/local/bin/scl_enable \
    ENV=/usr/local/bin/scl_enable \
    PROMPT_COMMAND=". /usr/local/bin/scl_enable"
ENV PATH="${PATH}:${GRADLE_HOME}/bin"

USER root

# Add default settigns.xml
COPY contrib/configure-slave /usr/local/bin/configure-slave
COPY contrib/configure-slave /usr/local/bin/scl_enable

# Make directories
RUN mkdir -p ${GRADLE_HOME} \
    && yum install -y centos-release-scl-rh \
    && wget -L -O /gradle.zip https://services.gradle.org/distributions/gradle-${VERSION}-bin.zip \
    && unzip /gradle.zip \
    && rm -f /gradle.zip \
    && chmod -R g+rwX ${GRADLE_HOME} \
    && yum clean all -y \
    && yum autoremove -y \
    && rm -rf /var/cache/yum

USER 1001
