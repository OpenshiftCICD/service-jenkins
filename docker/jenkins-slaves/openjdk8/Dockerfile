FROM openshift/jenkins-slave-base-centos7

MAINTAINER Thomas Herzog <herzog.thomas81@gmail.com>

# Arguments for java version
ARG VERSION_JAVA

# Remove openjdk
RUN yum remove -y java* \
    && yum install -y java-${VERSION_JAVA}-openjdk.x86_64 \
    && yum install -y centos-release-scl-rh

RUN yum clean all -y \
    && yum autoremove -y
