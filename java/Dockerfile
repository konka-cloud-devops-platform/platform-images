# ==================================
# Java Golden Runtime Image (UBI 9)
# ==================================

# Java Golden Runtime Image (UBI 9)
FROM redhat/ubi9-minimal:9.0.0

# Install Java 11 (headless) + user tools
RUN microdnf install -y \
        java-11-openjdk-headless \
        shadow-utils \
    && microdnf clean all

# JVM tuning
ENV JAVA_OPTS="-XX:+UseContainerSupport \
               -XX:MaxRAMPercentage=75.0 \
               -Djava.security.egd=file:/dev/./urandom"

LABEL org.opencontainers.image.source="platform-team" \
      org.opencontainers.image.description="Java Golden Runtime Image" \
      org.opencontainers.image.version="11-jre-ubi9-v1"

# Create non-root user
RUN useradd -r -u 1001 roboshop && \
    mkdir -p /opt/server && \
    chown -R roboshop:roboshop /opt/server

WORKDIR /opt/server
USER 1001

EXPOSE 8080

CMD ["sh", "-c", "java $JAVA_OPTS -jar app.jar"]

