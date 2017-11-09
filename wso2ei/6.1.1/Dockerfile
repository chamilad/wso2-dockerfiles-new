FROM ubuntu:16.04
MAINTAINER dev@wso2.org

ENV DEBIAN_FRONTEND noninteractive

ENV WSO2_SERVER=wso2ei \
    WSO2_SERVER_VERSION=6.1.1 \
    WSO2_SERVER_RUNTIME=integrator \
    CARBON_HOME=/opt/wso2ei-6.1.1 \
    JAVA_HOME=/opt/java

COPY wso2ei-6.1.1.zip /opt
COPY jdk-8u131-linux-x64.tar.gz /opt

WORKDIR /opt

RUN addgroup wso2 && \
    adduser --system --shell /bin/bash --gecos 'WSO2User' --ingroup wso2 --disabled-login wso2user && \
    apt-get update && \
    apt-get install -y --no-install-recommends --no-install-suggests wget zip unzip && \
    unzip wso2ei-6.1.1.zip && \
    tar zxvf jdk-8u131-linux-x64.tar.gz && \
    ln -s /opt/jdk1.8.0_131 java && \
# Cleanup
    rm -rf wso2ei-6.1.1.zip jdk-8u131-linux-x64.tar.gz && \
    apt-get purge -y --auto-remove wget zip unzip && \
    rm -rfv /var/lib/apt/lists/* && \
# Permissions
    chown -R wso2user:wso2 /opt/wso2ei-6.1.1 && \
    chown -R wso2user:wso2 /opt/jdk1.8.0_131

USER wso2user

CMD ["/opt/wso2ei-6.1.1/bin/integrator.sh"]
