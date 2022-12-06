# emojivoto

## Introduction

This chart will deploy a emojivoto instance in Kubernetes.

Emojivoto is a microservice application stack that allows users to vote for their favorite emoji, and tracks votes received on a leaderboard. May the best emoji win. This is based off of [BuoyantIO's Emojivoto example application.](https://github.com/BuoyantIO/emojivoto)

The application is composed of the following 3 services:

* [emojivoto-web](https://github.com/BuoyantIO/emojivoto/tree/main/emojivoto-web): Web frontend and REST API
* [emojivoto-emoji-svc](https://github.com/BuoyantIO/emojivoto/tree/main/emojivoto-emoji-svc/): gRPC API for finding and listing emoji
* [emojivoto-voting-svc](https://github.com/BuoyantIO/emojivoto/tree/main/emojivoto-voting-svc): gRPC API for voting and leaderboard

## Configuration

The following table lists the required values needed for the chart:

| Parameter               | Description                                                                                                  | Type   | Required                       |
|:------------------------|:-------------------------------------------------------------------------------------------------------------|:-------|:-------------------------------|
| `emojiReplicaCount`     | The number of replicas desired for the emoji service                                                         | int    | Yes                            |
| `webReplicaCount`       | The number of replicas desired for the web service                                                           | int    | Yes                            |
| `votebotReplicaCount`   | The number of replicas desired for the vote-bot. The more replicas the more load it will put on the services | int    | Yes                            |
| `injectLinkerd.enabled` | Enable automatic injection of linkerd proxy                                                                  | bool   | Yes                            |
| `externalDNS.enabled`   | Enable External DNS for Emojivoto. Cluster must have External DNS set up                                     | bool   | Yes                            |
| `ttl`                   | TTL value for your DNS provider                                                                              | string | If externalDNS.enabled is true |
| `hostname`              | Hostname you want external DNS to use for the Emojivoto frontend                                             | string | If externalDNS.enabled is true |



## Example values.yaml:

```
# Number of replicas for the emoji app
emojiReplicaCount: 3

# Number of replicas for the web app
webReplicaCount: 3

# Number of replicas for the vote-bot app
votebotReplicaCount: 10

# Enable Linkerd automatic inject
injectLinkerd:
  enabled: true

# If you have enabled external-dns with your kommander install you can enable automatic DNS registration for your services
externalDNS:
  enabled: false
  ttl: "Auto"
  hostname: 
``` 

---
