# Prometheus Setup Guide
This guide is designed to guide users to setting up the prometheus application for various exporters.

## Adding an exporter
The config file is located at ~/prometheus/prometheus.yml

To add a new exporter source, you must add a new entry to the bottom of the `prometheus.yml` file.

```yml
...
- job_name: 'node_exporter'
  static_configs:
    - targets: ['localhost:9101']
      labels:
        app: "node_exporter"
- job_name: 'dcgm_exporter'
  static_configs:
    - targets: ['chimera21:9401']
      labels:
        app: "dcgm_exporter"
- job_name: 'some name'
  static_configs:
    - targets: ['host name']
      labels:
        app: "some name"
```

You can verify that your exporter is accessible by curling the `/metrics`.

```
curl http://[hostname]:[exporter port number]
```


*Examples*
node exporter: `curl http://localhost:9100`
dcgm exporter: `curl http://chimera21:9401`
