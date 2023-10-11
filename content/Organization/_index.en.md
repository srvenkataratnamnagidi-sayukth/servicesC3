---
title: Organization
weight: 5
---
Since our inception, while we have aligned our thoughts, principles and ideas with changing times and newer market demands, but our core values that accentuate our standards of work and commitment to customers have been always drawn from the following unwavering guiding principles.
1. **Customer Centricity:** \
To relentlessly drive the quality, costs and delivery of our IT services and solutions with utmost customer centricity backed with prompt and proactive communication in order to provide supreme customer delight.
1. **Business Ethics and Transparency** \
To be honest, dedicated, fair, transparent, sincere and open in all our customer transactions.
1. **Respect** \
To hold our customers, partners, colleagues, and stakeholders in great esteem, dignity and prestige.
1. **Innovation** \
To continuously strive to be technologically innovative and achieve process excellence in order to enable our customers harvest significant business advantages.

## Reporting Structure
{{<mermaid align="left">}}
classDiagram
	Chairman <|-- CFO
	Chairman <|-- CEO
	CEO <|-- CTO
	CEO <|-- COO
	CEO <|-- CHRO
	CTO <|-- ED_Engg_SaaSPlatform
	CTO <|-- ED_Engg_MobilePlatform
	CTO <|-- ED_Engg_DevOps
	CTO <|-- ED_Engg_Innovation
	CTO <|-- ED_Doc_Tech
	COO <|-- ED_Ops_Datacenters
	COO <|-- ED_Ops_TechSupport
	CHRO <|-- ED_Ops_HR
	CFO <|-- ED_Finance_Accounts
	ED_Engg_SaaSPlatform <|-- EM_WEBAPP
	ED_Engg_SaaSPlatform <|-- EM_WEBAPI
	ED_Engg_MobilePlatform <|-- EM_MobileSurvey
	ED_Engg_MobilePlatform <|-- EM_MobileGOVT
	ED_Doc_Tech <|-- DM_All
	ED_Engg_Innovation <|-- Product_RnD_Developer1
	ED_Engg_Innovation <|-- Product_RnD_Developer2
	ED_Engg_Innovation <|-- Product_RnD_Developer3
	
	Chairman <|-- Director1
	Chairman <|-- Director2
	Chairman <|-- Director3
	Chairman <|-- Director4
	
{{< /mermaid >}}
{{% children  %}}
