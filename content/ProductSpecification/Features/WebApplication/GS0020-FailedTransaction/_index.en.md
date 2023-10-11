---
title: GS0020 - Failed Transaction
tags : ["Composing"]
---

## Introduction
While users making transaction, transaction gets failed or we cannot get response even transaction is successful. Failed Transaction is used to store the incomplete transactions. While knowing about status of transaction using gateway apis, we use this failed transaction. 

## Business Assumptions
Transactions data should be saved into database automatically.

## Requirements
### Functional Requirements
1. we will save incomplete transaction's data into the database.

### Non-functional Requirements
1. Database should work properly even if there are more records of incomplete transactions.

### Problem Statement
Failed Transaction feature is required to store the incomplete transactions. 

### Design 
1. Each failed transaction has pg type, pg vendor type, invoice id, payment_transaction id order id.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|

#### Use cases
|Use case Code|Description|
|-------------|-----------|


#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|----|----|------|-------|
|invoice|YES|NA|NA|@ManyToOne(fetch = FetchType.LAZY) @JoinColumn(name = "invoice_id",  referencedColumnName = "id")|invoice_id VARCHAR(36) NOT NULL|NO|NO|NO||
|paymentTransaction|YES|NA|NA|@ManyToOne(fetch = FetchType.LAZY) @JoinColumn(name = "payment_transaction_id",  referencedColumnName = "id")|payment_transaction_id VARCHAR(36) NOT NULL|NO|NO|NO||
|orderId|NO|NA|NA|@Column(name = "order_id", length = 128 ,nullable = true)|order_id VARCHAR(128) DEFAULT NULL|NO|NO|NO||
|pgtype|NO|NA|NA|@Enumerated(EnumType.STRING) @Column(name = "pgtype", length = 8 ,nullable = true)|pgtype varchar(8) DEFAULT NULL|NO|NO|NO||
|pgVendorType|NO|NA|NA|@Enumerated(EnumType.STRING) @Column(name = "pg_vendor_type", length = 8, nullable = true)|pg_vendor_type varchar(8) DEFAULT NULL|NO|NO|NO||
|paymentState|NO|NA|NA|@Enumerated(EnumType.STRING) @Column(name = "payment_state", length = 16, nullable = true)|payment_state varchar(16) DEFAULT NULL|NO|NO|NO||
|rzpResponseErrorCode|NO|NA|NA|@Column(name = "rzp_response_error_code", length = 64 ,nullable = true)|rzp_response_error_code VARCHAR(64) DEFAULT NULL|NO|NO|NO||
|rzpResponseErrorDescr|NO|NA|NA|@Column(name = "rzp_response_error_description", length = 256 ,nullable = true)|rzp_response_error_description VARCHAR(256) DEFAULT NULL|NO|NO|NO||
|rzpResponseErrorSource|NO|NA|NA|@Column(name = "rzp_response_error_source", length = 64 ,nullable = true)|rzp_response_error_source VARCHAR(64) DEFAULT NULL|NO|NO|NO||
|rzpResponseErrorStep|NO|NA|NA|@Column(name = "rzp_response_error_step", length = 64 ,nullable = true)|rzp_response_error_step VARCHAR(64) DEFAULT NULL|NO|NO|NO||
|rzpResponseErrorReason|NO|NA|NA|@Column(name = "rzp_response_error_reason", length = 64 ,nullable = true)|rzp_response_error_reason VARCHAR(64) DEFAULT NULL|NO|NO|NO||
|paytmStatus|NO|NA|NA|@Column(name = "paytm_status", length = 128 ,nullable = true)|paytm_status VARCHAR(128) DEFAULT NULL|NO|NO|NO||
|paytmRespCode|NO|NA|NA|@Column(name = "paytm_resp_code", length = 128 ,nullable = true)|paytm_resp_code VARCHAR(128) DEFAULT NULL|NO|NO|NO||
|paytmRespMsg|NO|NA|NA|@Column(name = "paytm_resp_msg", length = 1024 ,nullable = true)|paytm_resp_msg VARCHAR(1024) DEFAULT NULL|NO|NO|NO||
|paymentStep|NO|NA|NA|@Column(name = "payment_step", length = 8 ,nullable = true)|payment_step varchar(8) DEFAULT NULL|NO|NO|NO||
|retryExpired|NO|NA|NA|@Column(name = "retry_expired", nullable = true)|retry_expired boolean DEFAULT false|NO|NO|NO||
|retryCount|NO|0|NA|@Column(name = "retry_count", nullable = true)|retry_count bigint(20) DEFAULT '0'|NO|NO|NO||

#### Enum Constants

##### Payment Gateway Type

{{<mermaid align="left">}}
classDiagram
    class PgType{
      CASH
      CHALLAN
      ONLINE
      NONE
    }
{{< /mermaid >}}

##### Payment Gateway Vendor

{{<mermaid align="left">}}
classDiagram
    class PgVendorType{
      RAZORPAY
      PAYTM
      SBI
      NONE
    }
{{< /mermaid >}}

##### Payment State

{{<mermaid align="left">}}
classDiagram
    class PaymentState{
     PAID
     INITIATED
     FAILED
     REFUNDED
    }
{{< /mermaid >}}

#### Feature Permission
|Permission code|Action|
|---------------|-------|

#### Constraints
|Constraint|Key|
|----------|----|
|Primary Key|ID|

## Acceptance Criteria
|Permission|Description|
|-------------|-----------|

## User Experience

### List Page Buttons


### Flow Chart

{{<mermaid align="center">}}
%%{init: {'themeVariables': {'edgeLabelBackground':'#FFFF', 'tertiaryColor': '#fff0f0'}}}%%
graph TD
    Start((start))
    PaymentStatusWorker[PaymentStatusWorker]
    PaymentStatusService[PaymentStatusService]
    subgraph 5MinStatus Job
    5MinStatusJob[5MinStatusJob]
    PaymentStatusCmdHandler[PaymentStatusCmdHandler]
    5MinStatusJobLogic[Get data from paymentTransaction table with 1. state:initiated and retry:true and added_to_failed_transaction_table_check:false or <br> 2.payment state:Failed and retry:true and added_to_failed_transaction_table_check:false]
	5MinStatusJobEnd((Insert the payment transaction record into failed transaction table with retry_count:1))
    end
    subgraph 5Min Job
    5MinJob[5MinJob]
    FailedTransaction5MinCmdHandler[FailedTransaction5MinCmdHandler]
    5MinJobLogic[Get data from failedTransaction with retry_count:1]
    5MinJobIter{For each Object}
	5MinStatusIterBody[Check each order id payment status in payment gateway using api]
	5MinJobIter1{Payment Status}
	5MinJobEnd((Update object with retry:count:2 and save in failed transaction table))
	5MinJobEnd1((Update payment status in payment transaction table and failed transaction table))
    end
    subgraph 15Min Job
    15MinJob[15MinJob]
    FailedTransaction15MinCmdHandler[FailedTransaction15MinCmdHandler]
    15MinJobLogic[Get data from failedTransaction with retry_count:2]
    15MinJobIter{For each Object}
	15MinStatusIterBody[Check each order id payment status in payment gateway using api]
	15MinJobIter1{Payment Status}
	15MinJobEnd((Update object with retry:count:3 and save in failed transaction table))
	15MinJobEnd1((Update payment status in payment transaction table and failed transaction table))
    end
    subgraph 60Min Job
    60MinJob[60MinJob]
    FailedTransaction60MinCmdHandler[FailedTransaction60MinCmdHandler]
    60MinJobLogic[Get data from failedTransaction with retry_count:3]
    60MinJobIter{For each Object}
	60MinStatusIterBody[Check each order id payment status in payment gateway using api]
	60MinJobIter1{Payment Status}
	60MinJobEnd((Update object with retry:count:4 and save in failed transaction table))
	60MinJobEnd1((Update payment status in payment transaction table and failed transaction table))
    end
    subgraph 24Hr Job
    24HrJob[24HrJob]
    FailedTransaction24HrCmdHandler[FailedTransaction24HrCmdHandler]
    24HrJobLogic[Get data from failedTransaction with retry_count:4]
    24HrJobIter{For each Object}
	24HrStatusIterBody[Check each order id payment status in payment gateway using api]
	24HrJobIter1{Payment Status}
	24HrJobEnd((Update object with retry:count:5 and save in failed transaction table))
	24HrJobEnd1((Update payment status in payment transaction table and failed transaction table))
    end
    subgraph 48Hr Job
    48HrJob[48HrJob]
    FailedTransaction48HrCmdHandler[FailedTransaction48HrCmdHandler]
    48HrJobLogic[Get data from failedTransaction with retry_count:5]
    48HrJobIter{For each Object}
	48HrStatusIterBody[Check each order id payment status in payment gateway using api]
	48HrJobIter1{Payment Status}
	48HrJobEnd((Update object with retry:count:6 and retry_expired:true and save in failed transaction table))
	48HrJobEnd1((Update payment status in payment transaction table and delete record in failed transaction table))
    end
    Start---->PaymentStatusWorker
    PaymentStatusWorker---->PaymentStatusService
    PaymentStatusService---->5MinStatusJob
    5MinStatusJob---->PaymentStatusCmdHandler
    PaymentStatusCmdHandler---->5MinStatusJobLogic
    5MinStatusJobLogic---->5MinStatusJobEnd
    PaymentStatusService---->5MinJob
    5MinJob---->FailedTransaction5MinCmdHandler
    FailedTransaction5MinCmdHandler---->5MinJobLogic
    5MinJobLogic---->5MinJobIter
    5MinJobIter---->5MinStatusIterBody
    5MinStatusIterBody---->5MinJobIter1
    5MinJobIter1--No status-->5MinJobEnd
    5MinJobIter1--Status:Success/Failure-->5MinJobEnd1
    PaymentStatusService---->15MinJob
    15MinJob---->FailedTransaction15MinCmdHandler
    FailedTransaction15MinCmdHandler---->15MinJobLogic
    15MinJobLogic---->15MinJobIter
    15MinJobIter---->15MinStatusIterBody
    15MinStatusIterBody---->15MinJobIter1
    15MinJobIter1--No status-->15MinJobEnd
    15MinJobIter1--Status:Success/Failure-->15MinJobEnd1
    PaymentStatusService---->60MinJob
    60MinJob---->FailedTransaction60MinCmdHandler
    FailedTransaction60MinCmdHandler---->60MinJobLogic
    60MinJobLogic---->60MinJobIter
    60MinJobIter---->60MinStatusIterBody
    60MinStatusIterBody---->60MinJobIter1
    60MinJobIter1--No status-->60MinJobEnd
    60MinJobIter1--Status:Success/Failure-->60MinJobEnd1
    PaymentStatusService---->24HrJob
    24HrJob---->FailedTransaction24HrCmdHandler
    FailedTransaction24HrCmdHandler---->24HrJobLogic
    24HrJobLogic---->24HrJobIter
    24HrJobIter---->24HrStatusIterBody
    24HrStatusIterBody---->24HrJobIter1
    24HrJobIter1--No status-->24HrJobEnd
    24HrJobIter1--Status:Success/Failure-->24HrJobEnd1
    PaymentStatusService---->48HrJob
    48HrJob---->FailedTransaction48HrCmdHandler
    FailedTransaction48HrCmdHandler---->48HrJobLogic
    48HrJobLogic---->48HrJobIter
    48HrJobIter---->48HrStatusIterBody
    48HrStatusIterBody---->48HrJobIter1
    48HrJobIter1--No status-->48HrJobEnd
    48HrJobIter1--Status:Success/Failure-->48HrJobEnd1
{{< /mermaid >}}

### State Machine


### Sequence Diagram

## Unit Test Cases
|Product Version|UnitTest Id|Description|
|---------------|-----------|-----------|
||||
||||

## Security compliance check


## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1. Don't provide any information about the FAILED TRANSACTION in the User Manual. It's scope is limited to Developer Technical Documentation

## Feature/Defect list
|Feature/Defect ID|Link|Status|
|----|----|---|
|GS-0003|[GS-0003](https://shadkona.atlassian.net/browse/GS-0003)|Closed|


## References
1. [Spring Security](https://spring.io/projects/spring-security)
1. [Intro to Spring Security Expressions](https://www.baeldung.com/spring-security-expressions)
1. [Spring Security Role Based Access Authorization Example](https://www.journaldev.com/8748/spring-security-role-based-access-authorization-example)

## Development Estimations
|Release Tag|Feature/Defect ID|Scrum Deatils|Start date|End date|
|-----------|-----------------|-------------|----------|--------|
|2020OCT|GS-0002|Scrum 2020OCTs2|14 OCT 2020|28 OCT 2020|

## Feature Doneness Criteria
Check list for the Doneness criteria

|Metric|Unit Measure|Expected Result|Actual Result|Accepted?|Remarks|Approver|
|------|------------|---------------|-------------|---------|-------|----------|
|Acceptance Criteria Defined?|YES or NO|YES|YES|Accepted|All test cases passed|PM|
|Architecture Approved?|YES or NO|YES|YES|Accepted|Design is accepted|Architect|
|Coding Completed?|YES or NO|YES|YES|Completed|Completed|EM|
|Product Defects|Number|0|0|Accepted||EM|
|Unit Test Case Count?|Number|>5|8|Accepted|Tested|EM|
|Integration Test Cases Count|Number|>5|9|Accepted|Tested|EM|
|Sonar Vulnerabilities Count|Number|0|0|Accepted|validated|EM|
|Code Coverage|Number|>98%|99%|Accepted|Validated|EM|
|User Manual Verified?|YES or NO|YES|YES|Accepted|Validated|DocM|
|PenTest Defect Count?|Number|<2|0|Accepted|Validated|EM|
|PM Accepted?|YES or NO|YES|YES|Accepted|Good to go|PM|
|OM Accepted?|YES or NO|YES|YES|Accepted|Good to go|OM|
|Deployed to Staging?|YES or NO|YES|YES|Accepted|Good to go|EM|
|Deployed to Production?|YES or NO|YES|YES|Accepted|Good to go|OM|




 
