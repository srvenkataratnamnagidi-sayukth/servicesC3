---
title: Product Release 2020NOV
tags : ["Composing"]
---
## Planned Release Cycle
{{<mermaid align="left">}}
gantt
    title Planned Release Cycle
    excludes    weekends
    dateFormat  YYYY-MM-DD
    todayMarker on
    section Design
    Features & Design			:t1, 2020-10-01, 14d
    PM and Architect Approval	:t2, 2020-10-10, 10d
    section Development
    Development       			:t3, after t2, 12d
    section Quality
    Quality       				:t4, after t2, 18d
    section Staging
    Staging Update      		:t5, after t2, 24d
    Documentation	      		:t6, after t2, 24d
    section Deployment
    Rollout to production      	:t7, after t5, 5d
{{< /mermaid >}}

## Executed Release Cycle
{{<mermaid align="left">}}
gantt
    title Executed Release Cycle
    excludes    weekends
    dateFormat  YYYY-MM-DD
    todayMarker on
    section Design
    Features & Design			:crit, active, t1, 2020-10-03, 14d
    PM and Architect Approval	:t2, 2020-10-10, 12d
    section Development
    Development       			:t3, after t2, 12d
    section Quality
    Quality       				:t4, after t2, 18d
    section Staging
    Staging Update      		:t5, after t2, 24d
    Documentation	      		:t6, after t2, 24d
    section Deployment
    Rollout to production      	:t7, after t5, 5d
{{< /mermaid >}}


## Release Metrics
|Metric name|Estimated Metric value|Actual Metric value|Deviation value|Remarks|
|-----------|----------------------|-------------------|---------------|-------|
|Kick off Date|01 OCT 2020|03 OCT 2020|-02 days|Delayed due to Calendar not available for all the members|
|Design Completion| 20 OCT 2020|22 OCT 2020| -02 days|Due to more discussions|
|Development Start Date|10 OCT 2020|14 OCT 2020|-04 days|Due to Architect Approvals|
|Development Code Freeze Date|
|Testing Freeze Date|
|Defect fix Freeze Date|
|Finalyze the Feature and Defects|
|PM Demo and Certify Date|
|User manual Freeze date|
|Rollout Date|

## Retrospection Decisions
|Reporter|Improvement|Accepted?|Update process?|Org Engineering Order Proceedings owner|Status|
|--------|-----------|---------|---------------|---------------------------------------|------|



## Feature Set
|Feature/Defect ID|Feature or Defect|Story Points|Subject|Reporter (Customer or Internal)|Status (Completed or Partial)|Target(Customer or Platform)|
|-----------------|-----------------|------------|-------|-------------------------------|-----------------------------|----------------------------|  

{{% children  %}}
