# Dockerfiles collection

Collection Docker images I made for my personal use. Images are not posted on Dockerhub, so you can't pull it from there but you can grab the Dockerfiles if needed.

<!-- TOC -->
  * [Allure CMD + Groovy](#allure-cmd--groovy)
  * [KubeCTL + Helm + Helmfile](#kubectl--helm--helmfile)
  * [Maven + Chrome](#maven--chrome)
  * [SoapIO + Groovy](#soapio--groovy)
  * [Usage](#usage)
  * [Changelog](#changelog)
<!-- TOC -->
___
### Allure CMD + Groovy

Image based on **alpine:3.19.1** contains:

- Groovy 4.0.18
- AllureCMD 2.9.0

Tools can be found in `/home`.

### KubeCTL + Helm + Helmfile

Image based on **alpine:3.19.1** contains:

- KubeCTL 1.29.2
- Helm 3.14.2
- Helmfile 0.162.0
- Helm plugins:
  - Helm diff v3.9.2
  - Helm secrets v4.5.1
  - Helm git v0.15.1
- Sops 3.8.1

KubeCTL, Helm, Helmfile and Sops are installed in `/usr/local/bin`.

### Maven + Chrome

Image based on **maven:3.9.6-eclipse-temurin-11** contains:

- Chrome stable version
- Chromedriver latest stable version

### SoapUI + Groovy

Image based on **openJDK:11-jdk-slim** contains:
   
- SoapUI 5.7.2
- Groovy 4.0.18 

Groovy can be found in `/home/groovy`, SoapUI in `/home/soapui`.

## Usage

As this is a personal sandbox use at your own risk.

## Changelog

v1.3:
- added more dockerfiles, updated all versions
- extended readme

v1.2:
- update groovy version to 4.0.15, soapui to 5.7.1

v1.1:
- update groovy version to 4.0.7
- minor tweaks in dockerfile