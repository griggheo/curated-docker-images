FROM ghcr.io/codepraxis-io/ubuntu22.04:base

ENV DEBIAN_FRONTEND=noninteractive

USER root

# Install openjdk-17-jre
RUN apt update -y \
    && apt install openjdk-17-jre -y

# Cleanup
RUN rm -rf /var/lib/apt/lists/* /var/cache/apt/*

# Switch to non-root user
USER devsecops
