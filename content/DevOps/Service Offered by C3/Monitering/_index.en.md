---
title: Monitoring
weight: 1
---

 We need continuous monitoring because:
 
 1. Better network visibility & transparency

2. Facilitates rapid responses 

3. Minimize system downtime

 4. Assists with healthy business performance

 Continuous control monitoring is a automated process which devops person (or)anyone can observe and detect compliance issues and security threats during each phase of the devops pipeline.

## Grafana

It is a multi-platform open source analytics and interactive visualization web application.that allow you to analyze and display data from various sources in real time.it provides a powerful and flexible way to create interactive dashboards,graphs,charts for monitoring and analyzing metrics,logs,other time series data.

## Prometheus

It is a open source system monitoring and alerting tool which pull the metric from client server over http and place the data in to its local data base which works on the principle of time series data base.

>Prometheus only can pull (or) scrapes data can’t collect the data by its own.so we uses some tools to collect the data.


**Prometheus Architecture Diagram**

![](Prometheus.png)

## Pushgateway

Prometheus scrapes data from applications and services at regular intervals, but the job intervals are still too slow to capture valuable information for batch jobs which complete so quickly that their lifespans are shorter than the Prometheus scrape interval itself, making it impossible to capture metrics from them at runtime.

Prometheus Pushgateway is a component of Prometheus that helps collect metrics for extremely small jobs. Instead of waiting until the next Prometheus scrape interval, which may slow down the system, we choose to have these brief jobs push metrics to a Pushgateway. A Prometheus Pushgateway acts as a kind of intermediate gateway, storing these pushed metrics until the next scrape interval.

- The --persistence.file flag sets the file location where to pushing metrics.
- The Pushgateway exposes all pushed metrics via the /metrics endpoint. this can changed this with the --web.telemetry-path flag.

- By default, Pushgateway listens to port 9091. 

## Alerts

Alert actively monitor your metric data and trigger notification or actions based on predefined conditions. alerts are more proactive and can help you detect and respond to critical events or anomalies in your data.

## Thresholds

threshold in grafana refer to predefined boundaries or limits set on metric. they are used to visually highlight (or) mask specific ranges (or) values in your data.

Thresholds helps your quickly identify when a metric exceeds (or) falls below a certain threshold level.

> Thresholds provide a visual aid but do not trigger any notification or actions on their own.

## Prometheus Metrics

A Metric is a Quantative measure that helps in the assessment ,comparison,and tracking of operational statistics.

Prometheus collects as a timestamped set of changes recorded successively in fixed intervals.
This metric data is then exposed by prometheus using a combination of the metric names and labels.

## Exporter

These are Software components that Facilitate the collection of metrics from different systems and applications.

These exporters are deployed alongside the target system and provide an interface for metrics retrieval.

### Node Exporter	 - 5 Exporter 

```
3kosh-in-pod1a-lb01-ndexporter

3kosh-in-pod1a-mon01-ndexporter

3kosh-in-pod1a-node01-ndexporter

3kosh-in-pod1a-node02-ndexporter

3kosh-in-pod1a-node03-ndexporter
```
*In a Node Exporter dashboard in Grafana, you typically have multiple panels, each displaying different metrics or information about the system being monitored. Here's an explanation of some common panels you might find in a Node Exporter dashboard:*

**CPU Usage Panel:**

This panel displays the CPU usage metrics of the target machine(s) being monitored. It can show the overall CPU usage percentage or break it down by individual CPU cores or modes (user, system, idle, etc.).

**Memory Usage Panel:**

This panel provides information about the memory usage on the target machine(s). It may include metrics like total memory, used memory, free memory, and memory usage percentage.

**Disk Usage Panel:**

This panel shows the disk usage metrics, including total disk space, used space, and available space. It can provide an overview of the disk usage on the target machine(s) or specific disks or partitions.

**Network Traffic Panel:**

 This panel displays the network traffic metrics, such as incoming and outgoing network traffic (bytes/sec) or network packets (packets/sec). It can give you insights into the network activity of the monitored system.

 **Load Average Panel:**

 The load average panel shows the system load average metrics, indicating the average number of processes in the system's run queue over different time intervals (e.g., 1 minute, 5 minutes, 15 minutes). It helps you understand the system's workload and resource utilization.

**Process Metrics Panel:**

This panel provides information about specific processes running on the target machine(s). It can show metrics like CPU usage, memory usage, and other process-specific metrics. You can configure this panel to monitor specific processes of interest.

**System Uptime Panel:**

This panel displays the system uptime metric, indicating how long the target machine has been running since the last reboot. It gives you an overview of the system's stability.

**Custom Panels:**

 Depending on your monitoring requirements, you can create custom panels to display any specific metrics exposed by the Node Exporter or other system-level metrics you find relevant.


*These are just some examples of panels you may find in a Node Exporter dashboard. The exact panels and their configurations may vary based on your specific monitoring needs and the metrics you choose to track. Grafana provides a wide range of visualization options and customization features, allowing you to create panels that best suit your monitoring requirements*

### HAproxy Exporter

*In a HAProxy Exporter dashboard in Grafana, you typically have multiple panels that provide insights into the performance and status of your HAProxy load balancer. Here's an explanation of some common panels you might find in a HAProxy Exporter dashboard:*

**Frontend Metrics Panel:**

This panel displays metrics related to the frontend of your HAProxy instance. It can include metrics like request rate, connection rate, and active connections for each frontend configured in HAProxy. Monitoring these metrics helps you understand the incoming traffic and the load on your load balancer.

**Backend Metrics Panel:**

This panel shows metrics related to the backends configured in your HAProxy instance. It can include metrics like server status (UP/DOWN), server response time, and the number of active connections per server. Monitoring backend metrics helps you track the health and performance of your backend servers.

**Server Status Panel:**

This panel provides an overview of the status of all servers (backends) configured in your HAProxy instance. It can display a table or graph indicating the availability and status of each server (UP, DOWN, MAINT, etc.). This helps you quickly identify any servers that are offline or experiencing issues.

**Request Metrics Panel:**

This panel shows metrics related to the requests being handled by HAProxy. It can include metrics like the number of requests, request rate, and response codes (2xx, 3xx, 4xx, 5xx) returned by the load balancer. Monitoring request metrics helps you understand the overall traffic patterns and the performance of your HAProxy instance.

**Error Rate Panel:**

This panel displays the error rate of your HAProxy instance. It can include metrics such as the percentage of requests resulting in errors (4xx, 5xx). Monitoring the error rate helps you identify potential issues or misconfigurations that may affect the application's availability or performance.

**Session Metrics Panel:**

This panel provides insights into session-related metrics in HAProxy. It can include metrics like the number of sessions, session rate, and session duration. Monitoring session metrics helps you understand the behavior and workload of client sessions.

**Load Balancing Algorithms Panel:**

If you have multiple backends configured with different load balancing algorithms, this panel shows the distribution of requests across the backends. It can help you visualize and verify the load balancing behavior of your HAProxy configuration.

**Custom Panels:**

Depending on your specific monitoring requirements and the metrics provided by the HAProxy Exporter, you can create custom panels to display any additional metrics or information you find relevant. Grafana allows you to customize panels based on the specific needs of your HAProxy monitoring.

*These are some examples of panels you may find in a HAProxy Exporter dashboard in Grafana. The actual panels and their configurations may vary depending on your specific monitoring goals, the metrics provided by the HAProxy Exporter, and the features and configuration of your HAProxy load balancer. Grafana provides flexibility to create and 
customize panels to suit your monitoring needs.*

## MySQL Exporter

```
3kosh-in-pod1a-node01:9104

3kosh-in-pod1a-node02:9104

3kosh-in-pod1a-node03:9104
```

*In a MySQL Exporter dashboard in Grafana, you typically have multiple panels, each displaying different metrics or information related to the MySQL database being monitored. Here's an explanation of some common panels you might find in a MySQL Exporter dashboard:*

**Database Size Panel:**

This panel provides information about the size of the MySQL database. It may include metrics like total database size, size of individual tables or schemas, and data growth trends over time.


**Queries Per Second (QPS) Panel:**

This panel displays the number of queries executed per second in the MySQL database. It helps monitor the query load and identify any sudden spikes or abnormalities in query traffic.


**Connections Panel:**

This panel shows the number of active database connections over time. It can provide insights into the database's connection pool usage and help identify connection-related issues.


**Slow Queries Panel:**

This panel highlights slow or poorly performing queries in the MySQL database. It can display metrics like the number of slow queries, average query execution time, and the most time-consuming queries. Monitoring slow queries helps identify performance bottlenecks and optimize query performance.


**InnoDB Buffer Pool Usage Panel:**

 If you're using the InnoDB storage engine, this panel shows the usage of the InnoDB buffer pool. It can include metrics such as the buffer pool hit rate, buffer pool size, and buffer pool usage percentage. Monitoring the buffer pool usage helps optimize memory allocation for caching data.


**Replication Lag Panel:**

 If you have a MySQL replication setup, this panel displays the replication lag between the master and slave servers. It helps monitor the delay in replicating database changes and ensures the replication process is running smoothly.


**Table Indexing Panel:**

This panel provides insights into the indexing status of database tables. It can include metrics like index usage, index size, and fragmentation. Monitoring table indexing helps identify inefficient or missing indexes and optimize query performance.


**InnoDB Deadlocks Panel:**

This panel tracks the occurrence of InnoDB deadlocks in the database. It can display metrics such as the number of deadlocks, deadlock frequency, and affected queries. Monitoring deadlocks helps identify concurrency issues and ensure data integrity.


**Custom Panels:**

Depending on your specific monitoring requirements, you can create custom panels to display any other MySQL-specific metrics or information you find relevant. Grafana offers flexibility to visualize and monitor various aspects of the MySQL database based on your needs.


*These are just some examples of panels you may find in a MySQL Exporter dashboard in Grafana. The actual panels and their configurations may vary based on your specific monitoring goals, the metrics you choose to track, and the features provided by the MySQL Exporter you are using. Grafana allows you to customize and create panels to suit your monitoring requirements.*

## Black box exporter

We can monitor all the services mentioned below like

https://api.pod1.3kosh.in  :tomcat service

https://build.3kosh.in    :jenkins service

https://code.3kosh.in   :sonar qube

https://prodmon.3kosh.in   :Grafana service

https://prodmondb.3kosh.in   :Promotheus service

https://prodmongw.3kosh.in :pushgate way


>In this we can see ssl certificate expiry date and service status wheather it is up or down and http service codes,probe duration,dns lookup resolution panal also. 

*The Blackbox Exporter is a Prometheus exporter that allows you to probe endpoints over various network protocols (HTTP, HTTPS, TCP, ICMP, etc.) and collect metrics related to the connectivity and response times of those endpoints. In a Blackbox Exporter dashboard in Grafana, you can have several panels that provide insights into the probed endpoints. Here's an explanation of some common panels you might find in a Blackbox Exporter dashboard:*

**Endpoint Availability Panel:**

 This panel displays the availability status of the probed endpoints. It indicates whether the endpoints are up or down based on the probe results. It can show a simple "Up/Down" status or provide more detailed information, such as the percentage of successful probes.


**Response Time Panel:**

This panel shows the response time metrics of the probed endpoints. It provides information about how long it takes for the endpoint to respond to the probe requests. It may include metrics like average response time, minimum response time, maximum response time, and response time percentiles.


**Status Codes Panel:**

If the Blackbox Exporter is probing HTTP or HTTPS endpoints, this panel displays the distribution of HTTP status codes received from the endpoints. It can show the count or percentage of responses for each status code category (1xx, 2xx, 3xx, 4xx, 5xx, etc.). Monitoring status codes helps identify any errors or issues returned by the endpoints.


**DNS Resolution Panel:**

If the Blackbox Exporter is probing endpoints using DNS, this panel provides insights into DNS resolution. It can show metrics like DNS resolution time, success rate, and any errors encountered during resolution.


**TCP Connectivity Panel:**

 If the Blackbox Exporter is probing TCP endpoints, this panel displays the TCP connectivity status. It indicates whether the TCP connection was successful or if there were any errors or timeouts.


**ICMP Response Panel:**

If the Blackbox Exporter is probing endpoints using ICMP (ping), this panel shows the ICMP response metrics. It may include metrics like average round-trip time (RTT), packet loss percentage, and any errors encountered during the ICMP probes.

**Custom Panels:**

 Depending on your monitoring requirements, you can create custom panels to display any specific metrics or information collected by the Blackbox Exporter. This allows you to monitor and visualize additional aspects of the probed endpoints, such as SSL certificate expiration, specific headers in HTTP responses, or any other custom probes you have configured.


*These are some examples of panels you may find in a Blackbox Exporter dashboard in Grafana. The actual panels and their configurations may vary depending on your specific monitoring needs, the metrics collected by the Blackbox Exporter, and the protocols and probes you have configured. Grafana provides flexibility to customise and create panels based on the metrics you want to monitor from the probed endpoints.*


## Logs:
lots are textual records of events or activities that occur within a system or application. they capture information such as error messages, warnings, informational messages and other relevant events.,logs are typically human-readable and provide detailed information about specific events including timestamps, severity levels. error code, stack traces and contextual data. logs are useful for troubleshooting, debugging and understanding the sequence of event leading upto an issue.




{{% children  %}}












