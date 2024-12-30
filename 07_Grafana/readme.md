# Adding Grafana to an Elastic Cluster
## Why you might want to do this?
Grafana adds alerting capabilities without the need of a license.
Also its strong dashboard capabilities might be interesting for you.

## Installation

Use the existing ELK cluster that you already have.
Use the `docker-compose.yml` of this chapter to run a grafana instance.
You will connect Grafana via the UI to your ELK cluster.

Start the Grafana instance:
```
docker-compose up
```

or with newer Docker versions:
```
docker compose up
```