FROM alpine:3.24

ARG MISE_VERSION=v2026.11.12

# mise must be installed inside $PATH
RUN apk add curl git && \
    curl -fsSL https://mise.run | \
    MISE_INSTALL_PATH="/usr/local/bin/mise" \
    MISE_VERSION=${MISE_VERSION} sh

WORKDIR /mise

COPY config.ci.toml mise.ci.lock .mise/

# Configures mise to target CI environment
ENV MISE_ENV="ci"

RUN addgroup -S -g 1000 mise && \
    adduser -S -D -u 1000 -G mise mise && \
    chown -R mise:mise .

USER mise

RUN mise trust && mise install --locked --verbose
