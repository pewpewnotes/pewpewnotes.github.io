### Prometheus
* Prometheus is new kid in monitoring where he keeps the data in timeseries. Its pretty much same as icinga except more robust and easier to understand.
* My setup includes 2 VM machines (<3 vagrant)
1. VM 1: Debian -> IP based addition
2. VM 2: Debian -> IP based addition
* My plan is to use VM 1 to monitor multiple nodes.
* Install prometheus and node exporter on vm1, node exporter in 2.
* Setup the /etc/prometheus/prometheus.yml
```
# my global config
global:
  scrape_interval:     15s # Set the scrape interval to every 15 seconds. Default is every 1 minute.
  evaluation_interval: 15s # Evaluate rules every 15 seconds. The default is every 1 minute.
  # scrape_timeout is set to the global default (10s).

# Alertmanager configuration
alerting:
  alertmanagers:
  - static_configs:
    - targets:
      # - alertmanager:9093

# Load rules once and periodically evaluate them according to the global 'evaluation_interval'.
rule_files:
  # - "first_rules.yml"
  # - "second_rules.yml"

# A scrape configuration containing exactly one endpoint to scrape:
# Here it's Prometheus itself.
scrape_configs:
  # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
  - job_name: 'prometheus'

    # metrics_path defaults to '/metrics'
    # scheme defaults to 'http'.

    static_configs:
    - targets: ['localhost:9090']
    - targets: ['localhost:9100']
    - targets: ['192.168.0.101:9100']
```

