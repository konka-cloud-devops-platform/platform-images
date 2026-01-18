FROM alpine:3.23.2

LABEL org.opencontainers.image.source="platform-team" \
      org.opencontainers.image.description="Java Golden Runtime Image" \
      org.opencontainers.image.version="11-jre-alpine-3.23.2"

RUN addgroup -S roboshop && \
    adduser -S roboshop -G roboshop && \
    mkdir -p /opt/server && \
    chown -R roboshop:roboshop /opt/server && \
    apk add --no-cache \
        openjdk17-jre

ENV JAVA_HOME=/usr/lib/jvm/java-17-openjdk
ENV PATH=$JAVA_HOME/bin:$PATH

ENV JAVA_OPTS="-XX:+UseContainerSupport \
               -XX:MaxRAMPercentage=75.0 \
               -Djava.security.egd=file:/dev/./urandom"

WORKDIR /opt/server

USER roboshop

EXPOSE 8080

CMD ["sh", "-c", "java $JAVA_OPTS -jar app.jar"]
