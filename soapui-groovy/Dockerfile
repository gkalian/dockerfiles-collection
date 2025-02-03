FROM openjdk:11.0.16-jdk-slim

ENV GROOVY_VERSION=4.0.21 \
    SOAPUI_VERSION=5.7.2 \
    GROOVY_HOME="/home/groovy" \
    PATH="$PATH:/home/groovy/bin" \
    SOAPUI_HOME="/home/soapui"

RUN apt-get update \
      && apt-get install --no-install-recommends -y curl unzip \
      && apt-get clean \
      && rm -rf /var/lib/apt/lists/*

# https://groovy.apache.org/download.html
RUN curl -kLO https://archive.apache.org/dist/groovy/${GROOVY_VERSION}/distribution/apache-groovy-binary-${GROOVY_VERSION}.zip \
      && unzip "apache-groovy-binary-${GROOVY_VERSION}.zip" \
      && mv "/groovy-${GROOVY_VERSION}" "/home/groovy" \
      && rm apache-groovy-binary-${GROOVY_VERSION}.zip

# https://www.soapui.org/downloads/latest-release/
RUN curl -kLO https://dl.eviware.com/soapuios/${SOAPUI_VERSION}/SoapUI-${SOAPUI_VERSION}-linux-bin.tar.gz \
      && tar xf SoapUI-${SOAPUI_VERSION}-linux-bin.tar.gz \
      && mv SoapUI-${SOAPUI_VERSION} home/soapui \
      && rm SoapUI-${SOAPUI_VERSION}-linux-bin.tar.gz

WORKDIR /home/soapui