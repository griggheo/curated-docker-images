FROM ghcr.io/codepraxis-io/alpine3.16:run

USER root

# Install python and venv
RUN apk add python3 \
  && apk add py3-virtualenv

# Cleanup
RUN rm -rf /var/cache/apk/*

# switch to non-root user
USER devsecops
WORKDIR /home/devsecops
