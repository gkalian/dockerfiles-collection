FROM alpine:3.21.2

LABEL maintainer="https://github.com/gkalian"
LABEL description="Alpine-based image with Groovy and Allure Command Line for test reporting"

RUN apk update \
  && apk add --update --no-cache openjdk11 tzdata curl unzip bash git \
  && rm -rf /var/lib/apt/lists/*

# https://groovy.apache.org/download.html
ENV GROOVY_VERSION=4.0.21 \
    GROOVY_HOME="/home/groovy" \
    PATH="$PATH:/home/groovy/bin"

# https://repo.maven.apache.org/maven2/io/qameta/allure/allure-commandline/
ENV ALLURECMD_VERSION=2.29.0 \
    PATH="${PATH}:/home/allure-cmd/bin"

# Create a non-root user
RUN addgroup -S appgroup && adduser -S user -G appgroup

RUN curl -kLO https://archive.apache.org/dist/groovy/${GROOVY_VERSION}/distribution/apache-groovy-binary-${GROOVY_VERSION}.zip \
      && unzip "apache-groovy-binary-${GROOVY_VERSION}.zip" \
      && mv "/groovy-${GROOVY_VERSION}" "/home/groovy" \
      && rm apache-groovy-binary-${GROOVY_VERSION}.zip \
      && curl -kLO https://repo.maven.apache.org/maven2/io/qameta/allure/allure-commandline/${ALLURECMD_VERSION}/allure-commandline-${ALLURECMD_VERSION}.zip \
      && unzip "allure-commandline-${ALLURECMD_VERSION}.zip" \
      && mv "/allure-${ALLURECMD_VERSION}" "/home/allure-cmd" \
      && rm allure-commandline-${ALLURECMD_VERSION}.zip \
      && chown -R appuser:appgroup /home/groovy /home/allure-cmd

WORKDIR /home/groovy
USER user