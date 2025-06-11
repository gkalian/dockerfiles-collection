# Dockerfiles collection

Collection Docker images I made for my personal use. Images are not posted on Dockerhub, so you can't pull it from there but you can grab the Dockerfiles if needed.

<!-- TOC -->
- [Dockerfiles collection](#dockerfiles-collection)
    - [Allure CMD + Groovy](#allure-cmd--groovy)
    - [KubeCTL + Helm + Helmfile](#kubectl--helm--helmfile)
    - [Maven + Chrome](#maven--chrome)
    - [SoapUI + Groovy](#soapui--groovy)
  - [Usage](#usage)
  - [Changelog](#changelog)
<!-- TOC -->
___
### Allure CMD + Groovy

Image based on **alpine:3.22.0** contains:

- Groovy 4.0.27
- AllureCMD 2.34.0

Tools can be found in `/home`.

### KubeCTL + Helm + Helmfile

Image based on **alpine:3.22.0** contains:

- KubeCTL 1.33.0
- Helm 3.18.2
- Helmfile 0.170.0
- Helm plugins:
  - Helm diff v3.12.2
  - Helm secrets v4.6.5
  - Helm git v1.4.0
- Sops 3.810.2

KubeCTL, Helm, Helmfile and Sops are installed in `/usr/local/bin`.

### Maven + Chrome

Image based on **maven:3.9.9-eclipse-temurin-11** contains:

- Chrome stable version
- Chromedriver latest stable version

### SoapUI + Groovy

Image based on **openJDK:11-jdk-slim** contains:
   
- SoapUI 5.8.0
- Groovy 4.0.27

Groovy can be found in `/home/groovy`, SoapUI in `/home/soapui`.

## Usage

As this is a personal sandbox use at your own risk.

## Changelog

v1.8:
- versions updated (breaking change in helm git plugin - v.1.4.0)

v1.7:
- versions updated (no breaking changes)

v1.6:
- Labels added
- Optimized
- Github workflow updated

v1.5:
- Renovate bot added
- Github workflow added

v1.4:
- updated versions

v1.3:
- added more dockerfiles, updated all versions
- extended readme

v1.2:
- update groovy version to 4.0.15, soapui to 5.7.1

v1.1:
- update groovy version to 4.0.7
- minor tweaks in dockerfile
