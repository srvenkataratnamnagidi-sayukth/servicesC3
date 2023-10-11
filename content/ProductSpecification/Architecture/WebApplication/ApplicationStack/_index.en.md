---
title: Web Application Stack
weight: 5
tags: ["Composing"] 
---

## Activity
|Date|Reviewer|Reviewer Comments|Approver|Approver Remarks|
|----|--------|-----------------|--------|----------------|
|20 DEC 2020|[P C Varma](http://#)|Reviewed|[P C Varma](http://#)|Approved|

## Development Server

{{<mermaid align="left">}}
classDiagram
	OS *.. VM
	JDK *.. OS
	Tomcat *.. JDK
	HAProxy *.. Tomcat
	MySQL *.. OS
	ScyllaDB *.. OS
	MySQL <.. Tomcat
	ScyllaDB <.. Tomcat

	VM : VirtualBox 6.x
	OS : Centos 8
	JDK : OpenJDK11
	Tomcat : Tomcat 9
	HAProxy : HAProxy 2_3
	MySQL : MySQL 8_x
	
{{< /mermaid >}}

## Staging Server

{{<mermaid align="left">}}
classDiagram
	OS *.. GCP
	JDK *.. OS
	Tomcat *.. JDK
	HAProxy *.. Tomcat
	MySQL *.. OS
	ScyllaDB *.. OS
	MySQL <.. Tomcat
	ScyllaDB <.. Tomcat

	GCP : VM 
	OS : Centos 8
	JDK : OpenJDK11
	Tomcat : Tomcat 9
	HAProxy : HAProxy 2_3
	MySQL : MySQL 8_x
	
{{< /mermaid >}}

## Production Server

Pending
