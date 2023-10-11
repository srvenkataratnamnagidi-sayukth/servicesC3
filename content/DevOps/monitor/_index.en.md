---
title: Monitoring Requirements
tags : ["Composing"]
---

## Entities in the Deployments
Following Entities in all the Deployments

### Application Infra
+ Dell/HP Hardware
	+ Network Interface Cards
	+ Motherboard
	+ PSU or SMPS
	
+ OS Oracle Linux 
+ Kubernetes
+ Percona XtraDB Node
	+ Replication Status
	+ Number of nodes
+ Redpanda Node
	+ Replication Status
	+ Number of nodes
+ ScyllaDB Node
	+ Replication Status
	+ Number of nodes
+ HA Proxy
	+ Usage stats
	+ Under usage stats

### DevOps Infra
+ HA Proxy or nothing
+ Jenkins
+ PostgreSQL
+ SonarQube
+ Snyk check possibility

### Connectivity
+ ICMP Ping from from one server to another
+ TCP Port access from one server to another, if ICMP fails
+ P2P Link Connectivity

{{% children  %}}
