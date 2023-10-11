---
title: Basic Model
weight: 5
---
Every product has its own domain. Its our main responsibility to understand the following to develop a product that can help end user to do the business.
The following are the basic building blocks of this product

## Basic building blocks of the product
### User Persona
We have the following Personas identified in this product domain
This product documentation is centered around the following Personas
1. Panchayat Citizen
1. Panchayat level Property Owner
1. Panchayat level Property Owner's nominee
1. Panchayat Secretary
1. Panchayat Surpanch
1. Panchayat Revenue Officer
1. Panchayat Anaganvadi School Teacher
1. Mandal Panchayat Officer
1. Mandal Revenue Officer
1. Division Level Panchayat Officer
1. District Panchayat Officer
1. District Collector
1. State Commissioner
1. State Deputy Commissioner
1. State Level Bank Officer
1. State Level Police Officer
1. State Level Medical Service Officer
 
### Roles of Users
1. Panchayat Secretary
1. Panchayat President
1. Mandal PanchayatRaj Officer
1. Mandal Revenue Officer
1. Division Level PanchayatRaj Officer
1. District Panchayat Officer
1. State Deputy Commissioner
1. State Commissioner
1. State Minister
1. State Level Bank Officer
1. State Level Police Officer
1. State Level Medical Service Officer

### Feature Permissions
Every feature should be bound to a Permission if it touches C-U-R-V-E 
The following are the feature permissons in the product
Note : Please link all the Feature Permissions in this table

|Feature name|Link to respective feature|
|------------|--------------------------|
|Citizens|<Link>|

### Persistence Model
Every Feature will disected to a couple of small, independant, dis-joint & inherent Programmable objects to persist in the Database following [BCNF](https://beginnersbook.com/2015/05/normalization-in-dbms/) rules.
The following is the top level persistence model
Naming convention of this persistence model is **dao** (Data Access Object) 

{{<mermaid align="left">}}
classDiagram
	SearchableDo <|-- BaseDo
	AuditDo <|-- SearchableDo
	PropertyDo <|-- AuditDo
	OrgDo <|-- AuditDo

	BaseDo : #int version
	BaseDo : #String id
	BaseDo : #String classCode
	BaseDo : #String step
	BaseDo : #String captchaText
	BaseDo : #String mfaText
	 
	SearchableDo : #String captchaText
	SearchableDo : #Set~ObjectState~ objStateSet
	SearchableDo : #List~Long~ pageSizeList
	SearchableDo : #List~Long~ pageSizeList
	SearchableDo : #List~SearchableDo~ objList
	SearchableDo : #~TableNavigator~ tblNav
	SearchableDo : #List~SearchFilterElement~ filterList
	SearchableDo : #String sortParam
	SearchableDo : #Boolean sortOrder
	SearchableDo : #Long randomNumber
	
	AuditDo : #Date createdTime
	AuditDo : #Date updatedTime
	AuditDo : #Date sortedTime
	AuditDo : #String createdUserId
	AuditDo : #String updatedUserId
	AuditDo : #String updateComment
	AuditDo : #String removeComment
	AuditDo : #String createdUserName
	AuditDo : #String updatedUserName
	AuditDo : #~ObjectState~ objState
	AuditDo : #Date startCreatedTime
	AuditDo : #Date endCreatedTime
	AuditDo : #Date startUpdatedTime
	AuditDo : #Date endUpdatedTime
	AuditDo : #String wizardStep
	
	PropertyDo : #Property property
	PropertyDo : #String propertyId
	PropertyDo : #String propertyName
	
	OrgDo : #~Organization~ state
	OrgDo : #~Organization~ dist
	OrgDo : #~Organization~ div
	OrgDo : #~Organization~ mandal
	OrgDo : #~Organization~ panchayat
	OrgDo : #String orgNativeId
	
{{< /mermaid >}}

### Context of User Session  
This product has a User Context, i.e. Logged in user can have a different levels of the scopes described as follows. Each feature should have either FullContext(i.e. Need Panchayat selected) or OptionalContext.
This context selection should be based on the Context menu provide on top of the right content page.

|Level|State|District|Division|Mandal|Panchayat|
|-----|-----|--------|--------|------|---------|
|State User|NO|YES|YES|YES|YES|
|District User|NO|NO|YES|YES|YES|
|Division User|NO|NO|NO|YES|YES|
|Mandal User|NO|NO|NO|NO|YES|
|Panchayat User|NO|NO|NO|NO|NO|






