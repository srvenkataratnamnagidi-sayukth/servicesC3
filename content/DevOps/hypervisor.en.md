---
title: Hypervisor
tags: ["Composing"] 
---

## Hypervisor - Redhat KVM

Kernel-based Virtual Machine (KVM) is an open source virtualization technology built into Linux®. Specifically, KVM lets you turn Linux into a hypervisor that allows a host machine to run multiple, isolated virtual environments called guests or virtual machines (VMs).

KVM is part of Linux. If you’ve got Linux 2.6.20 or newer, you’ve got KVM. KVM was first announced in 2006 and merged into the mainline Linux kernel version a year later. Because KVM is part of existing Linux code, it immediately benefits from every new Linux feature, fix, and advancement without additional engineering.

## VM - Installed OS(hardden) Template
Decided OS is Oracle Linux 8.x as the OS for all the VMs and Hypervisors

## OS harden
Use CIS polcies to to secure the OS

[CIS Benchmark for Orcale Linux 8] (https://paper.bobylive.com/Security/CIS/CIS_Oracle_Linux_8_Benchmark_v2_0_0.pdf)

Some more links

+ https://github.com/Th3R0oT/Oracle-Enterprise-Linux-Security-Security_hardening-Infrastructure-Security-Audit
+ https://github.com/gurucp/cis_oel7_dev
+ https://github.com/mrC2C/cis-benchmark-centOS-8

## Creating a VM Template
### Procedure
The following links will describe how to create the VM and XML configuration file
Ref https://www.tecmint.com/create-kvm-virtual-machine-template/
Ref https://libvirt.org/formatdomain.html

### Boot sequence
- Step 1 : Install the VM with latest OS
- Step 2 : Update & Upgrade OS distribution
- Step 3 : harden the OS
- Step 4 : Install APP Stack
- Step 5 : Install App-Core

## How App-Core works?
Before we discuss "how the App-Core work lets?" understand the desired setup.

+ All the persistence Storage would be on VMs with the following Assumptions
	- Dedicated Data Disk for each type storage
		- /data/db for MySQL Database. The installations and configuration should be in the dedicated directory
		- /data/ds for ScyllaDB Datastore. The installations and configuration should be in the dedicated directory
		- /data/ms for Redpanda Message Stream. The installations and configuration should be in the dedicated directory
		- /data/mg for Hazelcast Memory Cache Service. The installations and configuration should be in the dedicated directory
	- Installation Environment should be different for Persistence ad Non-persistence nodes
		- e.g. ScyllaDB requires JDK 1.8 and Rest of the Services need JDK 17
		- Plan the conflicting dependancies and create the clusters accordingly
	- Estimated the following setup for the Production
		- MySQL XtraDB cluster
			- 5 Nodes Master - Master
				- MySQL XtraDB
				- 64 GB OS Disk  
				- 1 TB Data disk Usable
				- Permanent Data, Data Purging Policy
			- 3 Nodes Read Only cluster - Connected to Master-Master Cluster
				- MySQL XtraDB
				- 64 GB OS Disk
s				- 1 TB Data disk Usable
				- Permanent Data, Data Purging Policy
			- 7 Nodes RoundRobin 7 days. independant Node. Non-cluster, individual nodes. Daily Backup.
				- MySQL XtraDB
				- 64 GB OS Disk
				- 1 TB Data disk Usable
				- Permanent Data, Data Purging Policy
				- Every day mid-night Rotated
			- 3 Nodes RoundRobin 3 months. independant Node. Non-cluster, individual nodes. Monthly Backup.
				- MySQL XtraDB
				- 64 GB OS Disk
				- 1 TB Data disk Usable
				- Permanent Data, Data Purging Policy
				- Every Month first day of the month, mid-night Rotated
		- ScyllaDB cluster
			- 5 Nodes Master - Master
				- ScyllaDB Cluster
				- 64 GB OS Disk  
				- 2 TB Data disk Usable
				- Permanent Data, Data Purging Policy
			- 7 Nodes RoundRobin 7 days. independant Node. Non-cluster, individual nodes. Daily Backup.
				- MySQL XtraDB
				- 64 GB OS Disk
				- 2 TB Data disk Usable
				- Permanent Data, Data Purging Policy
				- Every day mid-night Rotated
			- 3 Nodes RoundRobin 3 months. independant Node. Non-cluster, individual nodes. Monthly Backup.
				- MySQL XtraDB
				- 64 GB OS Disk
				- 2 TB Data disk Usable
				- Permanent Data, Data Purging Policy
				- Every Month first day of the month, mid-night Rotated
		- Redpanda Message cluster
			- 5 Nodes Master - Master
				- Redpanda Cluster
				- 64 GB OS Disk  
				- 200 GB Data disk Usable
				- Temporary Data
		- Hazelcast Memory cluster
			- 5 Nodes Master - Master
				- Redpanda Cluster
				- 64 GB OS Disk  
				- Temporary Data
+ All the processing nodes would be on VMs with the following Assumptions
	- No dedicated Data Disk for each type storage
	- Estimated the following setup for the Production
		- 5 APP_WORKER Nodes
			- Open JDK 17.latest
			- 64 GB OS Disk
		- 5 API_WORKER Nodes
			- Open JDK 17.latest
			- 64 GB OS Disk
		- 3 NOTIFY_SMS_WORKER Nodes
			- Open JDK 17.latest
			- 64 GB OS Disk
		- 3 NOTIFY_EMAIL_WORKER Nodes
			- Open JDK 17.latest
			- 64 GB OS Disk
		- 3 NOTIFY_WHATSAPP_WORKER Nodes
			- Open JDK 17.latest
			- 64 GB OS Disk
		- 3 REPORT_WORKER Nodes
			- Open JDK 17.latest
			- 64 GB OS Disk
		- 3 PG_WORKER Nodes
			- Open JDK 17.latest
			- 64 GB OS Disk
		- 3 INVOICE_WORKER Nodes
			- Open JDK 17.latest
			- 64 GB OS Disk


|Node Type|Number|vCPU|Memory|OS Disk|Data Disk|Total vCPU|Total Memory|Total OS Disk|Total Data Disk|
|--|--|--|--|--|--|--|--|--|--|
|MYSQL CLUSTER-MASTER|5|4|8|64|0|20|40|320|0|
|MYSQL CLUSTER-NODE|3|4|8|64|0|20|40|320|0|
|MYSQL CLUSTER-ROUNDROBIN 7DAYS|7|4|8|64|0|20|40|320|0|
|MYSQL CLUSTER-ROUNDROBIN 3DAYS|3|4|8|64|0|20|40|320|0|
|SCYLLADB CLUSTER|5|4|8|64|0|20|40|320|0|
|SCYLLADB CLUSTER-ROUNDROBIN 7DAYS|7|4|8|64|0|20|40|320|0|
|SCYLLADB CLUSTER-ROUNDROBIN 3DAYS|3|4|8|64|0|20|40|320|0|
|REDPANDA|5|4|8|64|0|20|40|320|0|
|HAZELCAST|5|4|8|64|0|20|40|320|0|
|APP|5|4|8|64|0|20|40|320|0|
|API|5|4|8|64|0|20|40|320|0|
|NOTIFY_SMS|3|4|8|64|0|20|40|320|0|
|NOTIFY_EMAIL|3|4|8|64|0|20|40|320|0|
|NOTIFY_WHATSAPP|3|4|8|64|0|20|40|320|0|
|REPORT|3|4|8|64|0|20|40|320|0|
|PG|3|4|8|64|0|20|40|320|0|
|INVOICE|3|4|8|64|0|20|40|320|0|
## What is the App-Core
App-Core is a special controller in the VM that can be started every time the VM boots in to the OSs.
It will do the following configurations
+ Identify it's role from the 
	- Following are the different types of Roles
	- APP Server 
	- API Server
	- REPORT Server
	- NOTIFY_SMS Server
	- NOTIFY_EMAIL Server
	- NOTIFY_WHATSAPP Server
	- REPORT Server
+ 
