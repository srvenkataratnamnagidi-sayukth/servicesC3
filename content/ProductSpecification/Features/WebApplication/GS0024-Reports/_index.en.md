---
title: GS0024 - Reports
tags : ["Composing"]
---

## Introduction
Reports are used to store information about the types of reports our product supports(citizen/properties/invoice etc). User may want any type of report with custom attributes, we will generate report with selected custom attributes. Report transaction is used to store information about the generated reports. Download Report is used to store information about the each downloaded report and the user who downloads it.

## Business Assumptions
Data about types of reports should be inserted into gs_report table manually.

## Requirements
### Functional Requirements
1. Data about downloaded report should be saved into database automatically.

### Non-functional Requirements

### Problem Statement
Report transaction is used to store information about the generated reports.

### Design 
1. Each report transaction has a export type, report type, access level.
1. Each download report has a downloaded user, report transaction id, report id.

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|

#### Use cases
|Use case Code|Description|
|-------------|-----------|
|report_generate|To generate report|

### Report

#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|----|----|------|-------|
|csvFormat|NO|NA|NA|@Column(name = "csv_format", nullable = true)|csv_format boolean DEFAULT false|NO|NO|NO||
|pdfFormat|NO|NA|NA|@Column(name = "pdf_format", nullable = true)|pdf_format boolean DEFAULT false|NO|NO|NO||
|stateScope|NO|NA|NA|@Column(name = "state_scope", nullable = true)|state_scope boolean DEFAULT false|NO|NO|NO||
|distScope|NO|NA|NA|@Column(name = "dist_scope", nullable = true)|dist_scope boolean DEFAULT false|NO|NO|NO||
|divScope|NO|NA|NA|@Column(name = "div_scope", nullable = true)|div_scope boolean DEFAULT false|NO|NO|NO||
|mandalScope|NO|NA|NA|@Column(name = "mandal_scope", nullable = true)|mandal_scope boolean DEFAULT false|NO|NO|NO||
|panchayatScope|NO|NA|NA|@Column(name = "panchayat_scope", nullable = true)|panchayat_scope boolean DEFAULT false|NO|NO|NO||
|name|YES|NA|NA|@Column(name = "name", length = 64, nullable = false, unique = true)|name varchar(64) NOT NULL|NO|NO|NO||
|code|YES|NA|NA|@Column(name = "code", length = 64, nullable = false, unique = true)|code varchar(64) NOT NULL|NO|NO|NO||
|descr|YES|NA|NA|@Column(name = "descr", length = 256, nullable = false)|descr varchar(256) NOT NULL|NO|NO|NO||
|csvImgPath|YES|NA|NA|@Column(name = "csv_image_path", length = 36, nullable = false)|csv_image_path varchar(36) NOT NULL|NO|NO|NO||
|pdfImgPath|YES|NA|NA|@Column(name = "pdf_image_path", length = 36, nullable = false)|pdf_image_path varchar(36) NOT NULL|NO|NO|NO||
|resourcesSpec|YES|NA|NA|@Enumerated(EnumType.STRING) @Column(name = "resources_spec", length = 12, nullable = false)|resources_spec varchar(12) NOT NULL|NO|NO|NO||
|customAttributes|YES|NA|NA|@Column(name = "custom_attributes", length = 256, nullable = false)|custom_attributes varchar(256) NOT NULL|NO|NO|NO||

### Report Transaction

#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|----|----|------|-------|
|report|YES|NA|NA|@ManyToOne(fetch = FetchType.LAZY) @JoinColumn(name = "report_id")|report_id VARCHAR(36) NOT NULL|NO|NO|NO||
|exportType|YES|NA|NA|@Enumerated(EnumType.STRING) @Column(name = "export_type", length = 12, nullable = false)|export_type VARCHAR(12) NOT NULL|NO|NO|NO||
|reportType|YES|NA|NA|@Enumerated(EnumType.STRING) @Column(name = "report_type", length = 12, nullable = false)|report_type VARCHAR(12) NOT NULL|NO|NO|NO||
|genStatus|YES|NA|NA|@Enumerated(EnumType.STRING) @Column(name = "gen_status", length = 16, nullable = false)|gen_status VARCHAR(16) NOT NULL|NO|NO|NO||
|genStartTime|NO|NA|NA|@DateTimeFormat(pattern = "dd-MM-yyyy") @Temporal(TemporalType.TIMESTAMP) @Column(name = "gen_start_time", nullable = true)|gen_start_time datetime DEFAULT NULL|NO|NO|NO||
|genEndTime|NO|NA|NA|@DateTimeFormat(pattern = "dd-MM-yyyy") @Temporal(TemporalType.TIMESTAMP) @Column(name = "gen_end_time", nullable = true)|gen_end_time` datetime DEFAULT NULL|NO|NO|NO||
|filePath|NO|NA|NA|@Column(name = "file_path", length = 36, nullable = true)|file_path VARCHAR(36) DEFAULT NULL|NO|NO|NO||
|fileSize|NO|NA|NA|@Column(name = "file_size", nullable = true|file_size bigint(20) DEFAULT NULL|YES|YES|NO||
|accessLevel|YES|NA|NA|@Enumerated(EnumType.STRING) @Column(name = "access_level", length = 12, nullable = false)|access_level VARCHAR(12) NOT NULL|NO|NO|NO||
|reportExpTime|YES|NA|NA|@Enumerated(EnumType.STRING) @Column(name = "report_expiry_time", length = 12, nullable = false)|report_expiry_time VARCHAR(12) NOT NULL|NO|NO|NO||
|smsNotify|NO|NA|NA|@Column(name = "sms_notify", nullable = true)|sms_notify boolean DEFAULT false|NO|NO|NO||
|emailNotify|NO|NA|NA|@Column(name = "email_notify", nullable = true)|email_notify boolean DEFAULT false|NO|NO|NO||
|errorMsg|NO|NA|NA|@Column(name = "error_msg", length = 255, nullable = true)|error_msg VARCHAR(255) DEFAULT NULL|NO|NO|NO||
|selectedAttributes|YES|NA|NA|@Column(name = "selected_attributes", length = 1024, nullable = false)|selected_attributes VARCHAR(1024) NOT NULL|NO|NO|NO||
|reportStartTime|YES|NA|NA|@DateTimeFormat(pattern = "dd-MM-yyyy") @Temporal(TemporalType.TIMESTAMP) @Column(name = "report_start_date", nullable = false)|report_start_date datetime NOT NULL|NO|NO|NO||
|reportEndTime|YES|NA|NA|@DateTimeFormat(pattern = "dd-MM-yyyy") @Temporal(TemporalType.TIMESTAMP) @Column(name = "report_end_date", nullable = false)|report_end_date datetime NOT NULL|NO|NO|NO||

### Download Report 

#### Model Attributes
|Attribute name|Mandatory|Default value|Input Allowed Char set JSP/API|HSQL Column Definition|SQL Column Definition|View|List|Search|Remarks|
|--------------|---------|-------------|------------------------------|----------------------|---------------------|------|------|----|----|------|-------|
|report|YES|NA|NA|@ManyToOne(fetch = FetchType.LAZY) @JoinColumn(name = "report_id")|report_id VARCHAR(36) NOT NULL|NO|NO|NO||
|reportTransaction|YES|NA|NA|@ManyToOne(fetch = FetchType.LAZY) @JoinColumn(name = "report_transaction_id", nullable = false)|report_transaction_id VARCHAR(36) NOT NULL|NO|NO|NO||
|reportDownloadedUser|YES|NA|NA|@ManyToOne(fetch = FetchType.LAZY) @JoinColumn(name = "report_downloaded_user_id", nullable = false)|report_downloaded_user_id VARCHAR(36) NOT NULL|NO|NO|NO||
|reportDownloadedTime|YES|NA|NA|@DateTimeFormat(pattern = "dd-MM-yyyy") @Temporal(TemporalType.TIMESTAMP) @Column(name = "report_downloaded_time", nullable = true)|report_downloaded_time datetime NOT NULL|NO|NO|NO||


#### Enum Constants

##### Resource Spec

{{<mermaid align="left">}}
classDiagram
    class ResourceSpec{
      SMALL
      MEDIUM
      LARGE
    }
{{< /mermaid >}}

##### Report Generation Status

{{<mermaid align="left">}}
classDiagram
    class ReportGenStatus{
     INPROGRESS
     COMPLETED
     PENDING
    }
{{< /mermaid >}}

##### Access Level

{{<mermaid align="left">}}
classDiagram
    class AccessLevel{
      PRIVATE
      PUBLIC
    }
{{< /mermaid >}}

##### Export Type

{{<mermaid align="left">}}
classDiagram
    class ExportType{
      PDF
      EXCEL
    }
{{< /mermaid >}}

##### Report Type

{{<mermaid align="left">}}
classDiagram
    class ReportType{
      CITIZEN
    }
{{< /mermaid >}}

##### Report Expiry Time

{{<mermaid align="left">}}
classDiagram
    class ReportExpTime{
      ONE_WEEK
      ONE_DAY
      ONE_MONTH
      THREE_MONTHS
      SIX_MONTHS
      NINE_MONTHS
      ONE_YEAR
    }
{{< /mermaid >}}

#### Feature Permission
|Permission code|Action|
|---------------|-------|

#### Constraints

##### Report

|Constraint|Key|
|----------|----|
|Primary Key|ID|
|Unique Key|uk__gs_report__name (name)|
|Unique Key|uk__gs_report__code (code)|

##### Report Transaction

|Constraint|Key|
|----------|----|
|Primary Key|ID|
|Foreign Key|CONSTRAINT fk__gs_org_report_transaction__report_id FOREIGN KEY (report_id) REFERENCES gs_report (id)|

##### Download Report

|Constraint|Key|
|----------|----|
|Primary Key|ID|
|Foreign Key|CONSTRAINT fk__gs_org_report_download__report_downloaded_user_id FOREIGN KEY (report_downloaded_user_id) REFERENCES gs_user (id)|
|Foreign Key|CONSTRAINT fk__gs_org_report_download__report_id FOREIGN KEY (report_id) REFERENCES gs_report (id)|
|Foreign Key|CONSTRAINT fk__gs_org_report_download__report_transaction_id FOREIGN KEY (report_transaction_id) REFERENCES gs_org_report_transaction (id)|

## Acceptance Criteria
|Permission|Description|
|-------------|-----------|

## User Experience

### List Page Buttons


### Flow Chart



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
1. Don't provide any information about the Reports in the User Manual. It's scope is limited to Developer Technical Documentation

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




 
