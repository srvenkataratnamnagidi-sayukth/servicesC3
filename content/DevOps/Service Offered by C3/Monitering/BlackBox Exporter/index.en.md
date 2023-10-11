---
title : BlackBox Exporter
---

**BlackBox Exporter**


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
