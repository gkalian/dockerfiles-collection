FROM maven:3.9.9-eclipse-temurin-11

ENV TZ=Europe/Berlin
RUN ln -snf /usr/share/zoneinfo/${TZ} /etc/localtime && echo ${TZ} /etc/timezone

RUN apt-get update -qqy && apt-get install --no-install-recommends -qqy gpg unzip gnupg

RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
  && echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list \
  && apt-get update -qqy \
  && apt-get -qqy install --no-install-recommends google-chrome-stable \
  && rm /etc/apt/sources.list.d/google-chrome.list \
  && rm -rf /var/lib/apt/lists/* /var/cache/apt/* \
  && sed -i 's/"$HERE\/chrome"/"$HERE\/chrome" --no-sandbox/g' /opt/google/chrome/google-chrome

# ChromeDriver  https://googlechromelabs.github.io/chrome-for-testing/
RUN export CHROME_DRIVER_VERSION=$(curl -s https://googlechromelabs.github.io/chrome-for-testing/LATEST_RELEASE_STABLE) \
    && echo ${CHROME_DRIVER_VERSION} \
    && wget -q -O /tmp/chromedriver.zip https://storage.googleapis.com/chrome-for-testing-public/${CHROME_DRIVER_VERSION}/linux64/chromedriver-linux64.zip \
  && unzip /tmp/chromedriver.zip -d /opt \
  && rm /tmp/chromedriver.zip \
  && mv /opt/chromedriver-linux64/chromedriver /opt/chromedriver-${CHROME_DRIVER_VERSION} \
  && chmod 755 /opt/chromedriver-${CHROME_DRIVER_VERSION} \
  && ln -s /opt/chromedriver-${CHROME_DRIVER_VERSION} /usr/bin/chromedriver