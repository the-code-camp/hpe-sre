# Prometheus

[Prometheus](https://prometheus.io) is an open-source monitoring solution. It's a [CNCF](https://www.cncf.io) project (under the same foundation as Kubernetes), and it runs a whole suite of monitoring components.

## Reference

- [Prometheus documentation](https://prometheus.io/docs/introduction/overview/)
- [Download and installation details](https://prometheus.io/download/)
- [Configuration and service discovery](https://prometheus.io/docs/prometheus/latest/configuration/configuration/)
- [Prometheus HTTP API documentation](https://prometheus.io/docs/prometheus/latest/querying/api/)

## Run Prometheus

We'll run Prometheus in a Docker container:

- [prometheus.yml](./prometheus.yml) - is the container setup, publishing port 9090
- [config/prometheus.yml](./config/prometheus.yml) - is the Prometheus configuration file.

Start the container:

```
docker compose -f prometheus.yml up -d
```

> Browse to the Prometheus UI at http://localhost:9090

The default page lets you query metrics - we'll do that shortly. First check some other pages:

- http://localhost:9090/config (from the _Status...Configuration_ menu) - shows the config Prometheus is using
- http://localhost:9090/targets (from _Status...Targets_ menu) - shows the status of the scrape targets

None of the targets we want to monitor are running, but Prometheus will keep trying to find them.

This [Docker Compose file (apps.yml)](./apps.yml) starts some sample apps which app publish metrics. The containers will connect to the same Docker network as Prometheus, and they're using the DNS names Prometheus is expecting to find.

Run the apps:

```
docker compose -f apps.yml up -d
```

> Refresh the status page at http://localhost:9090/targets and you'll see the targets come online

Switch to the Graph page(http://localhost:9090/graph).

The simplest query just needs the metric name.
