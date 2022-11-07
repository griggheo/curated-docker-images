FROM ghcr.io/codepraxis-io/debian11:base

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update -y && \
    apt-get install --no-install-suggests --no-install-recommends --yes python3-venv libpython3-dev python3-pip \
    python3-distutils gcc

# install useful python modules
RUN pip3 install requests cyclonedx-bom

# Cleanup
RUN rm -rf /var/lib/apt/lists/* /var/cache/apt/*
