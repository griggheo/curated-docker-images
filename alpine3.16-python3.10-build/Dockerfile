FROM ghcr.io/codepraxis-io/alpine3.16:build

USER root

# Install python, pip and venv
RUN apk add python3 \
  && apk add python3-dev \
  && apk add py3-pip \
  && apk add py3-virtualenv

# install common python modules
RUN pip3 install requests \
  && pip3 install py-bcrypt

# Cleanup
RUN rm -rf /var/cache/apk/*

# /__w directory is used as workdir by GitHub Actions
RUN mkdir -p /__w \
  && chown devsecops:devsecops /__w
  
USER devsecops
WORKDIR /home/devsecops

