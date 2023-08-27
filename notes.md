# 1. WORK NOTES

- [1. WORK NOTES](#1-work-notes)
  - [1.1. structurizr-lite](#11-structurizr-lite)
  - [1.2. structurizr-cli](#12-structurizr-cli)
  - [1.3. trying for devcontainers](#13-trying-for-devcontainers)
  - [1.4. collating documentation styles](#14-collating-documentation-styles)


## 1.1. structurizr-lite
docker pull structurizr/lite

docker run -it --rm -p 8080:8080 -v ./structurizrdata:/usr/local/structurizr --name structurizr_lite -e STRUCTURIZR_WORKSPACE_PATH=structurizrworkspace1 -e STRUCTURIZR_WORKSPACE_FILENAME=sample structurizr/lite

## 1.2. structurizr-cli
docker pull structurizr/cli:latest

docker run -it --rm -v ./structurizrdata:/usr/local/structurizr --name structurizr_cli structurizr/cli export -w /usr/local/structurizr --format plantuml --output /usr/local/structurizr/cli/diagrams

## 1.3. trying for devcontainers

build faliled for docker image - docker build --no-cache -t my-image-name - < ./.devcontainer/Dockerfile.devcontainer

build hanged for docker image - docker build --no-cache -t my-image-name - < ./failed.devcontainer/Dockerfile.devcontainer

debug failed for common-debian.sh - tried to debug from ./failed.devcontainer/testscript.

## 1.4. collating documentation styles

- [archcolider](https://github.com/ldynia/archcolider)
- [sysops-squad](https://github.com/archkata2021t17/sysops-squad)
- [icedhacker](https://github.com/icedhacker/architecture-katas)
- [My Notion](https://www.notion.so/Framework-9f38c6d58f71420698b26fa2143b1ae1)