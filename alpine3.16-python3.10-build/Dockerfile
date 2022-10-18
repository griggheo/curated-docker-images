FROM ghcr.io/codepraxis-io/alpine3.16:build

USER root

# Install python, pip and venv
RUN apk add python3 \
  && apk add py3-pip \
  && apk add py3-virtualenv

# install common python modules
RUN pip3 install requests

# Cleanup
RUN rm -rf /var/cache/apk/*

# switch to non-root user
USER devsecops
