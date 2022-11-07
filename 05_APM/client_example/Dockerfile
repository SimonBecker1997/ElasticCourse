#Multi-Stage build

#Build application stage
#We need maven.
FROM maven:3.8.4-jdk-11
WORKDIR /usr/src/java-app

#build the application
ADD . /usr/src/java-code
WORKDIR /usr/src/java-code/opbeans

#Bring the latest frontend code
COPY --from=opbeans/opbeans-frontend:latest /app src/main/resources/public

RUN mvn -q --batch-mode package \
  -DskipTests \
  -Dmaven.repo.local=.m2 \
  --no-transfer-progress \
  -Dmaven.wagon.http.retryHandler.count=3 \
  -Dhttps.protocols=TLSv1.2 \
  -Dhttp.keepAlive=false \
  -Dmaven.javadoc.skip=true \
  -Dmaven.gitcommitid.skip=true
RUN cp -v /usr/src/java-code/opbeans/target/*.jar /usr/src/java-app/app.jar

#Run application Stage
#We only need java
FROM adoptopenjdk:14-jre-hotspot AS base

RUN export
RUN apt-get -qq update \
 && apt-get install --no-install-recommends -y -qq curl \
 && rm -f /var/cache/apt/archives/*.deb /var/cache/apt/archives/partial/*.deb /var/cache/apt/*.bin || true

WORKDIR /app
COPY --from=0 /usr/src/java-app/*.jar ./

# Copy Elastic agent from docker image
# updated by .ci/bump-version.sh
COPY --from=docker.elastic.co/observability/apm-agent-java:1.34.0 /usr/agent/elastic-apm-agent.jar /app/elastic-apm-agent.jar

#Download the opentelemetry agent
RUN curl -L https://github.com/open-telemetry/opentelemetry-java-instrumentation/releases/download/v1.10.1/opentelemetry-javaagent.jar --output /app/opentelemetry-javaagent.jar

# updated by .ci/bump-version.sh
LABEL \
    org.label-schema.schema-version="1.0" \
    org.label-schema.vendor="Elastic" \
    org.label-schema.name="opbeans-java" \
    org.label-schema.version="1.34.0" \
    org.label-schema.url="https://hub.docker.com/r/opbeans/opbeans-java" \
    org.label-schema.vcs-url="https://github.com/elastic/opbeans-java" \
    org.label-schema.license="MIT"

COPY ./start.sh .
RUN chmod +x ./start.sh
CMD ["./start.sh"]