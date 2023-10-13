---
title : PushGateWay
weight : 3
---

Prometheus scrapes data from applications and services at regular intervals, but the job intervals are still too slow to capture valuable information for batch jobs which complete so quickly that their lifespans are shorter than the Prometheus scrape interval itself, making it impossible to capture metrics from them at runtime.

Prometheus Pushgateway is a component of Prometheus that helps collect metrics for extremely small jobs. Instead of waiting until the next Prometheus scrape interval, which may slow down the system, we choose to have these brief jobs push metrics to a Pushgateway. A Prometheus Pushgateway acts as a kind of intermediate gateway, storing these pushed metrics until the next scrape interval.

- The --persistence.file flag sets the file location where to pushing metrics.
- The Pushgateway exposes all pushed metrics via the /metrics endpoint. this can changed this with the --web.telemetry-path flag.

- By default, Pushgateway listens to port 9091. 

## Push gateway Installation

### Install and Run Pushgateway

**Get the latest version of pushgateway from prometheus.io, then download and extract**
```
$ wget https://github.com/prometheus/pushgateway/releases/download/v0.8.0/pushgateway-0.8.0.linux-amd64.tar.gz
```
```
$ tar -xvf pushgateway-0.8.0.linux-amd64.tar.gz
```
### Create the pushgateway user
```
$ useradd --no-create-home --shell /bin/false pushgateway
```
### Move the binary in place and update the permissions to the user that we created:
```
$ cp pushgateway-0.8.0.linux-amd64/pushgateway /usr/local/bin/pushgateway
```
```
chown pushgateway:pushgateway /usr/local/bin/pushgateway
```
### Create the systemd unit file
```
$ cat > /etc/systemd/system/pushgateway.service << EOF
[Unit]
Description=Prometheus Pushgateway
Wants=network-online.target
After=network-online.target
[Service]
User=pushgateway
Group=pushgateway
Type=simple
ExecStart=/usr/local/bin/pushgateway
[Install]
WantedBy=multi-user.target
EOF
```
### Reload systemd and restart the pushgateway service:
```
$ systemctl daemon-reload
```
```
$ systemctl restart pushgateway
```
### Ensure that pushgateway has been started
```
$ systemctl status pushgateway
```
### Configure Prometheus
```
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'prometheus'
    scrape_interval: 5s
    static_configs:
      - targets: ['localhost:9090']

  - job_name: 'node_exporter'
    scrape_interval: 5s
    static_configs:
      - targets: ['localhost:9100']

  - job_name: 'pushgateway'
    honor_labels: true
    static_configs:
      - targets: ['localhost:9091']
```
```
$ systemctl restart prometheus
```