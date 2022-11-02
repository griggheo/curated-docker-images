FROM ghcr.io/codepraxis-io/alpine3.16:python3.10-build

ENV cosign_version=1.13.1
ENV crane_version=0.12.0
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

