---
title: Notify SMS Templates
weight: 5
---

## Notify SMS Template ID and Name

|Template ID|Name|
|-----------|----|
|1707161737313658477|OPEN|
|1707161348039346839|T00001_SUSR_SIGNUP|
|1707161348079998128|T00002_SUSR_ACT|
|1707161348088550611|T00003_SUSR_ACT_SUCC|
|1707162248223889285|SURVEYCOMPLETEDOTP|
|1707162248156828431|USERPASSWORDUPDATIONSUCCESSMSG|
|1707162248101675586|CERTIFICATESTATUSCHANGEDMSG|
|1707162248045408896|CERTIFICATECREATIONSUCCESSMSG|
|1707162247921711378|INVOICEGENERATEOTP|
|1707162247860247114|USERPASSWORDRESETOTP|
|1707162247570919888|SURVEYUSERACCOUNTACTIVATIONSUCCESS|
|1707162247490220500|SURVEYUSERENROLLEDSUCCESS|
|1707162244939248636|SURVEYUSERREGOTP|

### State Machine
NotifyLog object has the following state machine based on the attribute "state" 

{{<mermaid align="left">}}
flowchart LR
	Start((Start))
	Pending((Pending))
	Submitted((Submitted))
	Delivered((Delivered))
	Failed((Failed))
	Retry((Retry))
	Stop((Stop))
	
	Start --> Pending
	Pending --> Submitted
	Submitted --> Delivered
	Submitted --> Retry
	Retry --> Failed
	Retry --retry count  gt 5--> Retry
	Retry --> Delivered
	Delivered --> Stop
	Failed --> Stop
{{< /mermaid >}}

### Processing Flow chart
{{<mermaid align="left">}}
flowchart TD
	Start((Start))
	Pending((Pending))
	Submitted((Submitted))
	Delivered((Delivered))
	Failed((Failed))
	Retry((Retry))
	Stop((Stop))
	
	Start --> Pending
	Pending --> Submitted
	Submitted --> Delivered
	Submitted --> Retry
	Retry --> Failed
	Retry --retry count  gt 5--> Retry
	Retry --> Delivered
	Delivered --> Stop
	Failed --> Stop
{{< /mermaid >}}


{{% children  %}}
