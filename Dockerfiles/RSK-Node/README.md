## RSK Dockerfile

This repository contains **Dockerfile** of [RSK Node](http://www.rsk.co/) for [Docker](https://www.docker.com/)'s automated build. Is not published to the public [Docker Hub Registry](https://registry.hub.docker.com/).


### Base Docker Image

* [dockerfile/Ubuntu:Latest](https://hub.docker.com/_/ubuntu/)


### Installation

1. Install [Docker](https://docs.docker.com/engine/installation/).

2. Build the image from the Dockerfile:
  * MaiNet

  ```bash
 docker build -t mainnet -f Dockerfile.MainNet .
 ```
  * TestNet

  ```bash
  docker build -t testnet -f Dockerfile.TestNet .
  ```

  * RegTest

  ```bash
  docker build -t regtest -f Dockerfile.RegTest .
  ```

### Usage Examples
* MainNet

```bash
docker run -d --name mainnet-node-01  -p 4444:4444 -p 5050:5050 mainnet
```
* TestNet

```bash
docker run -d --name testnet-node-01  -p 4444:4444 -p 50505:50505 testnet
```
* RegTest

```bash
docker run -d --name regtest-node-01  -p 4444:4444 -p 30305:30305 regtest
```

Container comes with a default logback.xml (Dockerfiles/RSK-Node/rsk-logback.conf) and rsk.conf (Dockerfiles/RSK-Node/rsk-node.conf). The most important default values for rsk.conf are:

* configuration is for testnet network
* miner > client.enabled = false
* solc.path = /bin/false
* rpc > modules = allowed only eth and net
* rpc > cors = "\*"
* rpc > enabled = true
* rpc > port = 4444

If you wish to modify these, add the following flags to ```docker run``` command:

* -v /my/rsk-conf.conf:/etc/rsk/node.conf
* -v /my/rsk-logback.xml:/etc/rsk/logback.xml
