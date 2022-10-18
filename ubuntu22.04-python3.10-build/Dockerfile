FROM ghcr.io/codepraxis-io/ubuntu22.04:base

ENV DEBIAN_FRONTEND=noninteractive

USER root

# Install pip and venv
RUN apt-get update -y \
    && apt install python3-venv -y \
    && apt install python3-distutils -y \
    && apt install python3-pip -y

# install common python modules
RUN pip3 install requests

# Cleanup
RUN rm -rf /var/lib/apt/lists/* /var/cache/apt/*

# switch to non-root user
USER devsecops
