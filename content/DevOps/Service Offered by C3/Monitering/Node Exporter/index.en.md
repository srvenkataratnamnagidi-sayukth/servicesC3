---
title : Node Exporter
---

**Node Exporter**


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


