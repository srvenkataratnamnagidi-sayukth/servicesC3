---
title: Test Data Set
weight: 5
---
Every product has its own domain. Its our main responsibility to understand the following to develop a product that can help end user to do the business.
The following are the basic building blocks of this product

## Basic building blocks of the Tesing
### User Persona
We have the following Personas identified in this product domain
This product documentation is centered around the following Personas
1. Panchayat Level User
1. Mandal Level User
1. Division Level User
1. District Level User
1. State Level User
 
## Context Structure

{{<mermaid align="left">}}
graph TD
	State((State))
	District1((District1))
	District2((District2))
	Division1((Division11))
	Division2((Division12))
	Division3((Division21))
	Division4((Division22))
	Mandal1((Mandal111))
	Mandal2((Mandal112))
	Mandal3((Mandal121))
	Mandal4((Mandal122))
	Mandal5((Mandal211))
	Mandal6((Mandal212))
	Mandal7((Mandal221))
	Mandal8((Mandal222))
	Panchayat1((Panchayat1111))
	Panchayat2((Panchayat1112))
	Panchayat3((Panchayat1121))
	Panchayat4((Panchayat1122))
	Panchayat5((Panchayat1211))
	Panchayat6((Panchayat1212))
	Panchayat7((Panchayat1221))
	Panchayat8((Panchayat1222))
	Panchayat9((Panchayat2111))
	Panchayat10((Panchayat2112))
	Panchayat11((Panchayat2121))
	Panchayat12((Panchayat2122))
	Panchayat13((Panchayat2211))
	Panchayat14((Panchayat2212))
	Panchayat15((Panchayat2221))
	Panchayat16((Panchayat2222))
	State-->District1
	State-->District2
	District1-->Division1
	District1-->Division2
	District2-->Division3
	District2-->Division4
	Division1-->Mandal1
	Division1-->Mandal2
	Division2-->Mandal3
	Division2-->Mandal4
	Division3-->Mandal5
	Division3-->Mandal6
	Division4-->Mandal7
	Division4-->Mandal8
	Mandal1-->Panchayat1
	Mandal1-->Panchayat2
	Mandal2-->Panchayat3
	Mandal2-->Panchayat4
	Mandal3-->Panchayat5
	Mandal3-->Panchayat6
	Mandal4-->Panchayat7
	Mandal4-->Panchayat8
	Mandal5-->Panchayat9
	Mandal5-->Panchayat10
	Mandal6-->Panchayat11
	Mandal6-->Panchayat12
	Mandal7-->Panchayat13
	Mandal7-->Panchayat14
	Mandal8-->Panchayat15
	Mandal8-->Panchayat16
	

{{< /mermaid >}}

There are 5 levels of context. If we consider **binary tree** structure to create organizations for testing then the number of organizations would be 31. For every organization, there will be 2 users. One user will have **All** user permissions and another user will have **void** user permission. The loginname format for the District1 authorised user is **user_district1_authorised@gmail.com** i.e. (User will have **All** user permissions) and format for District1 Unauthorised user is **user_district1_unauthorised@gmail.com** i.e. (User will have **void** user permission).

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






