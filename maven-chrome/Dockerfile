FROM maven:3.9.11-eclipse-temurin-11

LABEL maintainer="https://github.com/gkalian"
LABEL description="Maven image with Chrome and ChromeDriver for web testing"

# Set shell options for better error handling
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

ENV TZ=Europe/Berlin
RUN ln -snf /usr/share/zoneinfo/"${TZ}" /etc/localtime && echo "${TZ}" > /etc/timezone

# Create a non-root user
RUN groupadd -r appgroup && useradd -r -g appgroup -m user

# Install Chrome - using wget consistently
RUN apt-get update -qqy && \
    apt-get install --no-install-recommends -qqy gpg unzip gnupg wget && \
    wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
    echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list && \
    apt-get update -qqy && \
    apt-get -qqy install --no-install-recommends google-chrome-stable && \
    rm /etc/apt/sources.list.d/google-chrome.list && \
    rm -rf /var/lib/apt/lists/* /var/cache/apt/* && \
    sed -i 's/"$HERE\/chrome"/"$HERE\/chrome" --no-sandbox/g' /opt/google/chrome/google-chrome

# ChromeDriver - using wget instead of curl for consistency
# https://googlechromelabs.github.io/chrome-for-testing/
RUN CHROME_DRIVER_VERSION=$(wget -q -O - https://googlechromelabs.github.io/chrome-for-testing/LATEST_RELEASE_STABLE) && \
    echo "${CHROME_DRIVER_VERSION}" && \
    wget -q -O /tmp/chromedriver.zip "https://storage.googleapis.com/chrome-for-testing-public/${CHROME_DRIVER_VERSION}/linux64/chromedriver-linux64.zip" && \
    unzip /tmp/chromedriver.zip -d /opt && \
    rm /tmp/chromedriver.zip && \
    mv /opt/chromedriver-linux64/chromedriver "/opt/chromedriver-${CHROME_DRIVER_VERSION}" && \
    chmod 755 "/opt/chromedriver-${CHROME_DRIVER_VERSION}" && \
    ln -s "/opt/chromedriver-${CHROME_DRIVER_VERSION}" /usr/bin/chromedriver && \
    chown -R user:appgroup /home/user

USER user
WORKDIR /home/user