---
title: Promotheus
weight : 2
---

 **Promotheus**

It is a open source system monitoring and alerting tool which pull the metric from client server over http and place the data in to its local data base which works on the principle of time series data base.

>Prometheus only can pull (or) scrapes data can’t collect the data by its own.so we uses some tools to collect the data.

**Prometheus Features**:

Prometheus's main features are:

- A multi-dimensional data model with time series data identified by metric name and key/value pairs
- PromQL, a flexible query language to leverage this dimensionality
- No reliance on distributed storage; single server nodes are autonomous
- time series collection happens via a pull model over HTTP
- Pushing time series is supported via an intermediary gateway
- Targets are discovered via service discovery or static configuration
- Multiple modes of graphing and dashboarding support


## Prometheus Installation

### Prerequisites


1.Deploy a fully updated Vultr Ubuntu 20.04 LTS

2.At least 2GB of RAM and 1 vCPU

3.SSH access with sudo privileges

 ## Update the System

Update the apt package list to prepare the system for further installations.

```
$ sudo apt update
```

## Download and Install Prometheus

Download the Prometheus release package.

```
$ wget https://github.com/prometheus/prometheus/releases/download/v2.27.1/prometheus-2.27.1.linux-amd64.tar.gz
```
 Extract the downloaded archive.

```
$ tar xvf prometheus-2.27.1.linux-amd64.tar.gz
```
 Change directory to the extracted archive.

```
$ cd prometheus-2.27.1.linux-amd64
```

 Create the configuration file directory.

```
$ sudo mkdir -p /etc/prometheus
```

 Create the data directory.

```
$ sudo mkdir -p /opt/prometheus/prometheus-data
```

Move the binary files prometheus and promtool to /usr/local/bin/.

```
$ sudo mv prometheus promtool /usr/local/bin/
```
 Move console files in console directory and library files in console_libraries directory to /etc/prometheus/ directory.

```
$ sudo mv consoles/ console_libraries/ /etc/prometheus/
```
 Move the template configuration file prometheus.yml to /etc/prometheus/ directory

```
$ sudo mv prometheus.yml /etc/prometheus/prometheus.yml
```

 Verify the installed version of Prometheus.

```
$ prometheus --version
```
 Verify the installed version of promtool.

```
$ promtool --version
```
## Configure System Group and User

 Create a prometheus group.

```
$ sudo groupadd --system prometheus
```

 Create a user prometheus and assign it to the created prometheus group.

```
$ sudo useradd -s /sbin/nologin --system -g prometheus prometheus
```

 Set the ownership of Prometheus files and data directories to the prometheus group and user.

```
$ sudo chown -R prometheus:prometheus /etc/prometheus/  /var/lib/prometheus/
```
```
$ sudo chmod -R 775 /etc/prometheus/ /var/lib/prometheus/
```
## Configure Systemd Service

 Create a systemd service file for Prometheus to start at boot time.

```
$ sudo nano /etc/systemd/system/prometheus.service
```
 Add the following lines to the file and save it:
```
[Unit]
Description=Prometheus
Wants=network-online.target
After=network-online.target

[Service]
User=prometheus
Group=prometheus
Restart=always
Type=simple
ExecStart=/usr/local/bin/prometheus \
    --config.file=/etc/prometheus/prometheus.yml \
    --storage.tsdb.path=/var/lib/prometheus/ \
    --web.console.templates=/etc/prometheus/consoles \
    --web.console.libraries=/etc/prometheus/console_libraries \
    --web.listen-address=0.0.0.0:9090

[Install]
WantedBy=multi-user.target
```

 Start the Prometheus service.
```
$ sudo systemctl start prometheus
```
 Enable the Prometheus service to run at system startup.

```
$ sudo systemctl enable prometheus
```
 Check the status of the Prometheus service.

```
$ sudo systemctl status prometheus
```

## Access Your Server

Access the Prometheus interface through your browser at port 9090. For example:

```
http://ip address:9090
``` 
 















