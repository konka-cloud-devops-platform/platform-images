# ===============================
# Build stage (uwsgi in venv)
# ===============================
FROM alpine:3.23.2 AS build

RUN apk add --no-cache \
    python3 \
    py3-pip \
    python3-dev \
    build-base \
    pcre-dev \
    libffi-dev \
    linux-headers

# Create virtual environment
RUN python3 -m venv /venv
ENV PATH="/venv/bin:$PATH"

# Install uwsgi inside venv (PEP 668 compliant)
RUN pip install --no-cache-dir uwsgi

# ===============================
# Runtime stage (clean & secure)
# ===============================
FROM alpine:3.23.2

ENV PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1 \
    PATH="/venv/bin:$PATH"

LABEL org.opencontainers.image.source="platform-team" \
      org.opencontainers.image.description="Python 3.12 Golden Runtime Image" \
      org.opencontainers.image.version="python3.12-alpine-3.23.2"

RUN apk add --no-cache \
    python3 \
    pcre \
    libffi \
    && addgroup -S roboshop \
    && adduser -S roboshop -G roboshop \
    && mkdir -p /opt/server \
    && chown -R roboshop:roboshop /opt/server

WORKDIR /opt/server

# Copy virtualenv from build stage
COPY --from=build /venv /venv

USER roboshop

EXPOSE 8080
CMD ["uwsgi", "--version"]