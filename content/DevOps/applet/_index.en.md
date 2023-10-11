---
title: Applet
tags : ["Composing"]
---

## What is the end goal?
+ Collect the Number of Servers in the different Datacenters. 
+ Monitor those servers using Hardware, OS and Application KPIs
+ Alert based on the Monitor thresholds
+ Monitor StartXi Metrics
+ Alert based on the StartXi thresholds

## What Technologies can be used?
+ Grafana
+ Promethius
+ Promethius Proxy
+ QuestDB
+ Graphite
+ Kiabana for logs or Grafana Loki
+ Grafana k6 for load testing

## What is Applet?
Applet is a peice of code that can be embedded in to a OS or an Application like Java application to monitor the target subject.
Applet will have 5 main things
+ Configuration
+ Code to schedule the Tasks
+ Code to monitor the Subject, monitoring will be primary & optional task
+ Remediation task
+ Inventory of the Subject

## Next steps
Lets do the RnD and find out a best Integration for Shadkona. We can use this as new Concept to mesure the StartXi.


{{% children  %}}
