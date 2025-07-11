FROM openjdk:11.0.16-jdk-slim

LABEL maintainer="https://github.com/gkalian"
LABEL description="SoapUI with Groovy for API testing and automation"

ENV GROOVY_VERSION=4.0.27 \
      SOAPUI_VERSION=5.8.0 \
      GROOVY_HOME="/home/groovy" \
      PATH="$PATH:/home/groovy/bin" \
      SOAPUI_HOME="/home/soapui"

# Create a non-root user
RUN groupadd -r appgroup && useradd -r -g appgroup -m user

RUN apt-get update \
      && apt-get install --no-install-recommends -y curl unzip \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

# https://groovy.apache.org/download.html
# https://www.soapui.org/downloads/latest-release/
RUN curl -kLO https://archive.apache.org/dist/groovy/${GROOVY_VERSION}/distribution/apache-groovy-binary-${GROOVY_VERSION}.zip \
      && unzip "apache-groovy-binary-${GROOVY_VERSION}.zip" \
      && mv "/groovy-${GROOVY_VERSION}" "/home/groovy" \
      && rm apache-groovy-binary-${GROOVY_VERSION}.zip \
      && curl -kLO https://dl.eviware.com/soapuios/${SOAPUI_VERSION}/SoapUI-${SOAPUI_VERSION}-linux-bin.tar.gz \
      && tar xf SoapUI-${SOAPUI_VERSION}-linux-bin.tar.gz \
      && mv SoapUI-${SOAPUI_VERSION} /home/soapui \
      && rm SoapUI-${SOAPUI_VERSION}-linux-bin.tar.gz \
      && chown -R user:appgroup /home/groovy /home/soapui

USER user
WORKDIR /home/soapui