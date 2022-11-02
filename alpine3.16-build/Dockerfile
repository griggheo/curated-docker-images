FROM ghcr.io/codepraxis-io/library/alpine:3.16

ENV cosign_version=1.13.1
ENV crane_version=0.12.0

# Install basic tools
RUN set -eux \
    #&& apk --no-cache add alpine-sdk \
    && apk --no-cache add \
    bash \
    build-base \
    ca-certificates \
    curl \
    docker-cli \
    gettext \
    git \
    gnupg \
    gpg-agent \
    jq \
    lsof \ 
    unzip \
    vim \
    wget \
    zip

# install cosign
RUN \
cd /tmp \
&& wget "https://github.com/sigstore/cosign/releases/download/v${cosign_version}/cosign-linux-amd64" \
&& mv cosign-linux-amd64 /usr/local/bin/cosign \
&& chmod +x /usr/local/bin/cosign

# install crane and gcrane
RUN \
mkdir -p /tmp/crane \
&& cd /tmp/crane \
&& curl -sL "https://github.com/google/go-containerregistry/releases/download/v${crane_version}/go-containerregistry_Linux_x86_64.tar.gz" > go-containerregistry.tar.gz \
&& tar xvfz go-containerregistry.tar.gz \
&& mv *crane /usr/local/bin \
&& crane version \
&& gcrane version \
&& cd /tmp \
&& rm -rf crane

# add user with UID and GID 1000 to be used instead of root
ENV USER_ID=1000
ENV GROUP_ID=1000
ENV USER_NAME=devsecops
ENV GROUP_NAME=devsecops
ENV USER_HOMEDIR=/home/devsecops

RUN addgroup -g ${GROUP_ID} ${GROUP_NAME} \
    && adduser -u ${USER_ID} -G ${GROUP_NAME} -D -h ${USER_HOMEDIR} ${USER_NAME}

# Cleanup
RUN rm -rf /var/cache/apk/*

# Switch to non-root user
#USER devsecops

