# ===============================
# Node.js Golden Platform Image
# ===============================
FROM alpine:3.23.2

# Runtime defaults
ENV NODE_ENV=production

LABEL org.opencontainers.image.source="platform-team" \
      org.opencontainers.image.description="Node.js Golden Runtime Image" \
      org.opencontainers.image.version="20-alpine-3.23.2"

# Install runtime first
RUN apk add --no-cache \
    nodejs-current \
    npm

# Create user and directories
RUN addgroup -S roboshop && \
    adduser -S roboshop -G roboshop && \
    mkdir -p /opt/server && \
    chown -R roboshop:roboshop /opt/server

WORKDIR /opt/server

# Drop root
USER roboshop

EXPOSE 8080

# Default command (developer overrides)
CMD ["node"]

