FROM jenkins/inbound-agent:latest-jdk11

ARG ENGINE_VERSION=1.0-rc66.0edcb5079f9e
ARG ENGINE_LOCATION="https://repo.jenkins-ci.org/artifactory/releases/io/jenkins/plugins/remoting-opentelemetry-engine/$ENGINE_VERSION/remoting-opentelemetry-engine-$ENGINE_VERSION.jar"
ARG ENGINE_PATH=/usr/share/remoting-otel/engine.jar
ARG LOG_PROP_PATH=/usr/share/remoting-otel/logging.properties
ARG user=jenkins

USER root
COPY logging.properties $LOG_PROP_PATH
RUN curl $ENGINE_LOCATION -o $ENGINE_PATH

USER $user

ENV JAVA_OPTS "-javaagent:$ENGINE_PATH -Djava.util.logging.config.file=$LOG_PROP_PATH ${JAVA_OPTS:-}"

ENTRYPOINT ["sh", "-c", "SERVICE_INSTANCE_ID=$JENKINS_AGENT_NAME /usr/local/bin/jenkins-agent"]
