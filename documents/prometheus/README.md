
# Prometheus

The Prometheus node exporter opens an endpoint on the Chimera head that scrapes CPU metrics via http://localhost:9101/metrics. The node exporter is deployed using tmux.

## Installation

Download the latest prometheus and node_exporter tar files [here](https://prometheus.io/download/)

Extract both tar files by running this command
```bash
tar xvfz prometheus-*.tar.gz
tar -xvf node_exporter-*.tar.gz
```

Check if everything is working by running this command
```bash
curl http://localhost:9101/metrics
```

### Configure the prometheus yaml file 

job_name helps group specific targets for prometheus to scrape. In this case we are scraping the dcgm_exporter located on chimera21 and node_exporter deployed on chimera head node. 

We are also making it available for Grafana to query metrics from Prometheus via port 9090. 

```
# my global config
global:
  scrape_interval: 15s # Set the scrape interval to every 15 seconds. Default i$
  evaluation_interval: 15s # Evaluate rules every 15 seconds. The default is ev$
  # scrape_timeout is set to the global default (10s).

# Alertmanager configuration
alerting:
  alertmanagers:
    - static_configs:
        - targets:
          # - alertmanager:9093

# Load rules once and periodically evaluate them according to the global 'evalu$
rule_files:
  # - "first_rules.yml"
  # - "second_rules.yml"

# A scrape configuration containing exactly one endpoint to scrape:
# Here it's Prometheus itself.
scrape_configs:
  # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
  - job_name: "prometheus"

    # metrics_path defaults to '/metrics'
    # scheme defaults to 'http'.

    static_configs:
      - targets: ["localhost:9090"]
       # The label name is added as a label `label_name=<label_value>` to any timeseries scraped from this config.
           labels:
          app: "prometheus"

    # Add this new job
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
```


## Prometheus Dashboard and Node exporter

The Prometheus dashboard can be found via http://localhost:9090/query

The status of each target endpoints can be found via http://localhost:9090/targets

In order to access the Prometheus dashboard in the browser. We will port forward :9090 to our local machine. 

Start up a local terminal and run this command. You can keep this terminal open with a tmux session.
```bash
ssh -L 9090localhost:9090 deploy@ip_address
```