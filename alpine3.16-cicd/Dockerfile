FROM ghcr.io/codepraxis-io/alpine3.16:python3.10-build

ENV ko_version=0.12.0

# Install basic tools
RUN set -eux \
    #&& apk --no-cache add alpine-sdk \
    && apk --no-cache add \
    bash \
    ca-certificates \
    curl \
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

# install ko
RUN \
mkdir -p /tmp/ko \
&& cd /tmp/ko \
&& curl -sL "https://github.com/ko-build/ko/releases/download/v${ko_version}/ko_${ko_version}_Linux_x86_64.tar.gz" > ko.tar.gz \
&& tar xvfz ko.tar.gz \
&& mv ko /usr/local/bin \
&& ko version \
&& cd /tmp \
&& rm -rf ko

# install trivy
RUN \
curl -sfL https://raw.githubusercontent.com/aquasecurity/trivy/main/contrib/install.sh | sh -s -- -b /usr/local/bin v0.34.0

# install semgrep
RUN \
python3 -m pip install semgrep

# install grype
RUN \
curl -sSfL https://raw.githubusercontent.com/anchore/grype/main/install.sh | sh -s -- -b /usr/local/bin \
&& chmod +x /usr/local/bin/grype
    
# install syft
RUN \
curl -sSfL https://raw.githubusercontent.com/anchore/syft/main/install.sh | sh -s -- -b /usr/local/bin \
&& chmod +x /usr/local/bin/syft

# Add $HOME/go/bin to $PATH
RUN \
echo 'PATH=$PATH:$HOME/go/bin' >> /root/.bashrc

# Cleanup
RUN rm -rf /var/cache/apk/*

# Switch to non-root user
#USER devsecops

