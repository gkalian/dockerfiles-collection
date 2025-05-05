FROM alpine:3.21.3

LABEL maintainer="https://github.com/gkalian"
LABEL description="Alpine-based image with kubectl, Helm, Helmfile and related tools for Kubernetes deployment"

RUN apk update --no-cache && \
    apk add --no-cache wget git

# Create a non-root user
RUN addgroup -S appgroup && adduser -S user -G appgroup

# https://kubernetes.io/releases/
ARG KUBECTL_VERSION=1.32.4
RUN wget "https://storage.googleapis.com/kubernetes-release/release/v${KUBECTL_VERSION}/bin/linux/amd64/kubectl" --quiet --output-document=/usr/local/bin/kubectl \
  && chmod +x /usr/local/bin/kubectl \
  && kubectl version --client --output=yaml 2>&1 | grep -q "${KUBECTL_VERSION}"

# https://github.com/helm/helm/releases
ARG HELM_VERSION=3.17.3
RUN wget "https://get.helm.sh/helm-v${HELM_VERSION}-linux-amd64.tar.gz" --quiet --output-document=/tmp/helm.tgz \
  && tar zxf /tmp/helm.tgz --strip-components 1 -C /usr/local/bin/ \
  && rm -f /tmp/helm.tgz

# https://github.com/helmfile/helmfile/releases
ARG HELMFILE_VERSION=0.170.0
RUN wget "https://github.com/helmfile/helmfile/releases/download/v${HELMFILE_VERSION}/helmfile_${HELMFILE_VERSION}_linux_amd64.tar.gz" --quiet --output-document=/tmp/helmfile.tgz \
  && tar --extract --gzip --verbose --file=/tmp/helmfile.tgz --directory=/usr/local/bin helmfile \
  && rm -f /tmp/helmfile.tgz

# https://github.com/databus23/helm-diff/releases
# https://github.com/jkroepke/helm-secrets/releases
# https://github.com/aslafy-z/helm-git/releases
ARG HELM_DIFF_VERSION=v3.11.0
ARG HELM_SECRETS_VERSION=v4.6.4
ARG HELM_GIT_VERSION=v0.17.0
RUN helm plugin install https://github.com/databus23/helm-diff --version ${HELM_DIFF_VERSION} && \
    helm plugin install https://github.com/jkroepke/helm-secrets --version ${HELM_SECRETS_VERSION} && \
    helm plugin install https://github.com/aslafy-z/helm-git.git --version ${HELM_GIT_VERSION}

# https://github.com/getsops/sops/releases
ARG SOPS_VERSION=3.10.2
RUN wget https://github.com/getsops/sops/releases/download/v${SOPS_VERSION}/sops-v${SOPS_VERSION}.linux.amd64 -O /usr/local/bin/sops \
    && chmod +x /usr/local/bin/sops

RUN kubectl version --client=true && \
    helm version && \
    helmfile --version && \
    chown -R user:appgroup /home/user

USER user
WORKDIR /home/user