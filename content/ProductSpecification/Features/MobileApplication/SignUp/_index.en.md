---
title: Sign Up
tags : ["Composing"]
---

## Introduction
Sign up is one of the basic features of the software product which contains confidential data. The product can be used by different users at various levels of the organization. 
To access the application, every user should sing up for the application. The sign up page allows a user to register in application by entering organization required data.

## Business Assumptions
1. Sign Up feature should be planned at the design phase.
1. Only employees of 2 survey companies should sign up for the application .
1. Sign Up user should provide organization required data when sign up for the application.Ex Name, E-Mail, Date Of Birth, Gender, Education Details, etc.

## Requirements
### Functional Requirements
1. Required a valid Username. Username is an email.
1. Required a password. Password should maintain format. The format is **a minimum of eight characters, at least one uppercase letter, one lowercase letter, one number, and one special character**.
1. Password and confirm Password fields value should be same.


### Non-functional Requirements
1. User should allow Phone, Contacts, Camera, Location and Storage permissions.

### Problem Statement
The sign up feature is required to register in the application, user should provide organization required data for registration.

### Design 
1. Sign up feature contains slides of sign up guide information.
1. After reading the sign-up information slides, and click on the **Get Started** button navigates the user to SignUp form page.  
1. After filling all required fields with data and click on **NEXT** button navigates the user to UserConfirmation page.
1. In the UserConfirmation page, after accepting the terms & conditions and click on **SEND OTP** button navigates the user to OTP Verification page.
1. After entering the correct phone SMS OTP and Email SMS OTP and click on the **CONFIRM** button navigates the user to SignUpSuccess Page.
1. To again receive SMS OTP & Email OTP, click on the **RESEND OTP** button if previous SMS OTP & Email OTP s are expired.
1. In the SignUpSuccess page, click on the **OK** button navigates the user to the Login page. 

#### Dependant Features
|Feature name|Reference Link|Remarks|
|------------|--------------|-------|
|Terms & Conditions|-|After accepting **terms & conditions** only user should continue the remaining sign-up process.|
|Home|-|Parent Page|
#### Use cases 
|Use case Code|Description|
|-------------|-----------|
|uc_sign_up_guide|Sign Up guide for registration.|
|uc_sign_up_form|To fill organization required data for sign up.|
|uc_sing_up_next_button|To navigate to UserConfirmation details page.|
|uc_sign_up_user_confirmation_page|To view UserConfirmation details.|
|uc_terms_and_condition_btn|To navigate to Terms & Conditions page.|
|uc_sign_up_terms_and_conditions_checkbox|To accept terms & conditions.|
|uc_sign_up_send_otp_btn|To confirm the user filled data and navigate to OtpVerification page|
|uc_sign_up_user_confirmation_back_btn| To navigate back to Sign Up form page and correct wrongly filled data.|
|uc_otp_confirm_btn|For otp verification and on success navigates user to SignUpSuccess page|
|uc_resend_otp_btn| To again receive SMS OTP & Email OTP and to continue the Sign Up process|
|uc_sign_up_success_ok_btn| To complete Sign Up process and navigates the user to Login Page|
 
 
#### Model Attributes
| Attribute name    | Mandatory | Default value | Input Allowed Char set Layout/API | SQLite Column Definition | Create | Update | Remove | View | List | Search | Remarks |
|-------------------|-----------|---------------|-----------------------------------|--------------------------|--------|--------|--------|------|------|--------|---------|
| id                | YES       | NA            | a-zA-Z0-9, maxlen=128             | id String                | NA     | NA     | NA     | NO   | NO   | NO     ||
| state             | YES       | NA            | a-zA-Z0-9, maxlen=128             | state String             | NA     | NA     | NA     | NO   | NO   | NO     ||
| hostnameApp       | YES       | NA            | a-zA-Z0-9, maxlen=128             | hostnameApp String       | NA     | NA     | NA     | NO   | NO   | NO     ||
| hostnameApd       | YES       | NA            | a-zA-Z0-9, maxlen=128             | hostnameApd String       | NA     | NA     | NA     | NO   | NO   | NO     ||
| hostnameApi       | YES       | NA            | a-zA-Z0-9, maxlen=128             | hostnameApi String       | NA     | NA     | NA     | NO   | NO   | NO     ||
| expiryTime        | YES       | NA            | a-zA-Z0-9, maxlen=128             | expiryTime Long          | NA     | NA     | NA     | NO   | NO   | NO     ||
| surveyCompanyList | YES       | NA            | a-zA-Z0-9, maxlen=128             | surveyCompanyList String | NA     | NA     | NA     | NO   | NO   | NO     ||

| Attribute name      | Mandatory | Default value | Input Allowed Char set Layout/API       | KV Database Key | SQLite Column Definition  | Create | Update | Remove | View | List | Search | Remarks                                     |
|---------------------|-----------|---------------|-----------------------------------------|-----------------|---------------------------|--------|--------|--------|------|------|--------|---------------------------------------------|
| otpUuid             | YES       | NA            | 0-9, maxlen=12                          | OTP_UUID        | otpUuid String            | YES    | NO     | NA     | NO   | NA   | NA     |                                             |
| otpTxId             | YES       | NA            | 0-9, maxlen=12                          | OTP_TXID        | otpTx String              | YES    | NO     | NA     | NO   | NA   | NA     |                                             |
| aadharId            | YES       | NA            | 0-9, maxlen=12                          | NA              | aadharId String           | YES    | YES    | YES    | YES  | NA   | NA     |                                             |
| name                | YES       | NA            | a-z A-Z, maxlen=64                      | NA              | name String               | YES    | YES    | YES    | YES  | NA   | NA     |                                             |
| surName             | YES       | NA            | a-z A-Z, maxlen=32                      | NA              | surName String            | YES    | YES    | YES    | YES  | NA   | NA     |                                             |
| spouseName          | YES       | NA            | a-zA-Z /, maxlen=64                     | NA              | spouseName String         | YES    | YES    | YES    | YES  | NA   | NA     |                                             |
| gender              | YES       | Male          | a-zA-Z0-9, maxlen=NA                    | NA              | gender String             | YES    | YES    | YES    | YES  | NA   | NA     |                                             |
| dob                 | YES       | NA            | 0-9/-, maxlen=10                        | NA              | dob String                | YES    | YES    | YES    | YES  | NA   | NA     |                                             |
| age                 | YES       | NA            | 0-9, maxlen=3                           | NA              | age String                | YES    | YES    | YES    | YES  | NA   | NA     |                                             |
| martialStatus       | YES       | Choose        | a-zA-Z, maxlen=NA                       | NA              | martialStatus String      | YES    | YES    | YES    | YES  | NA   | NA     |                                             |
| address             | YES       | NA            | a-zA-Z0-9. /-@&amp;_#,:;()/\, maxlen=64 | NA              | address String            | YES    | YES    | YES    | YES  | NA   | NA     |                                             |
| mobileNumber        | YES       | NA            | 0-9, maxlen=10                          | MOBILE          | mobileNumber String       | YES    | YES    | YES    | YES  | NA   | NA     | Getting from the Phone(No need to Enter)    |
| mobileNumber2       | NO        | NA            | 0-9, maxlen=10                          | NA              | mobileNumber2 String      | NO     | NA     | NA     | NO   | NA   | NA     | Inserting Default value "" in Database      |
| mobileNumber3       | NO        | NA            | 0-9, maxlen=10                          | NA              | mobileNumber3 String      | NO     | NA     | NA     | NO   | NA   | NA     | Inserting Default value "" in Database      |
| email               | YES       | NA            | a-zA-Z0-9. /-@&amp;_#,:;()/\, maxlen=64 | EMAIL           | email String              | YES    | YES    | YES    | YES  | NA   | NA     |                                             |
| email2              | NO        | NA            | a-zA-Z0-9. /-@&amp;_#,:;()/\, maxlen=64 | NA              | email2 String             | NO     | NA     | NA     | NO   | NA   | NA     | Inserting Default value "" in Database      |
| email3              | NO        | NA            | a-zA-Z0-9. /-@&amp;_#,:;()/\, maxlen=64 | NA              | email3 String             | NO     | NA     | NA     | NO   | NA   | NA     | Inserting Default value "" in Database      |
| os                  | NO        | NA            | NA                                      | NA              | os String                 | NA     | NA     | NA     | YES  | NA   | NA     | Inserting Default value Android in Database |
| osver               | YES       | NA            | a-zA-Z0-9, maxlen=64                    | NA              | osver String              | NA     | NA     | NA     | YES  | NA   | NA     |                                             |
| mobile manufacturer | YES       | NA            | a-zA-Z0-9, maxlen=64                    | NA              | mobileManufacturer String | NA     | NA     | NA     | YES  | NA   | NA     |                                             |
| model               | YES       | NA            | a-zA-Z0-9, maxlen=128                   | NA              | model String              | NA     | NA     | NA     | YES  | NA   | NA     |                                             |
| devUuid             | YES       | NA            | a-zA-Z0-9, maxlen=128                   | NA              | devUuid String            | NA     | NA     | NA     | YES  | NA   | NA     |                                             |
| geoLat              | YES       | NA            | a-zA-Z0-9, maxlen=128                   | NA              | geoLat String             | YES    | YES    | YES    | YES  | NA   | NA     |                                             |
| geoLng              | YES       | NA            | a-zA-Z0-9, maxlen=128                   | NA              | geoLng String             | YES    | YES    | YES    | YES  | NA   | NA     |                                             |
| surveyCompanyName   | YES       | Choose        | a-zA-Z, maxlen=NA                       | NA              | surveyCompanyName String  | YES    | YES    | YES    | YES  | NA   | NA     |                                             |
| image               | YES       | NA            | a-zA-Z0-9, maxlen=128                   | NA              | image String              | YES    | YES    | YES    | YES  | NA   | NA     |                                             |
| userPassword        | YES       | NA            | a-zA-Z0-9. /-@&amp;_#,:;()/\, maxlen=64 | NA              | userPassword String       | YES    | YES    | YES    | YES  | NA   | NA     |                                             |
| confirmPassword     | YES       | NA            | a-zA-Z0-9. /-@&amp;_#,:;()/\, maxlen=64 | NA              | confirmPassword String    | YES    | YES    | YES    | YES  | NA   | NA     |                                             |
| tshirtSize          | YES       | Choose        | a-zA-Z, maxlen=NA                       | NA              | tshirtSize String         | YES    | YES    | YES    | YES  | NA   | NA     |                                             |


#### Feature Permission
No feature permission for this Sign Up feature.

|Permission code|Action|
|---------------|-------|
|-|-|
|-|-|

## Acceptance Criteria
||
|--|
|Version : 1.0||
|1. The user who have correct Aadhaar details, Email and phone number can able to sign for the application|

## User Experience
### Home page
{{<mermaid align="left">}}
graph LR 
    SignUpBtn[Sign Up Button]
{{< /mermaid >}}

### Sign Up Guide page
{{<mermaid align="left">}}
graph LR 
    GetStartedBtn[Get Started]
{{< /mermaid >}}

### Sign Up form page
{{<mermaid align="left">}}
graph LR 
    SignUpNextBtn[Next Button]-->BackBtn[Back Button]
{{< /mermaid >}}

### Sign Up User Confirmation page
{{<mermaid align="left">}}
graph LR 
    SendOtpBtn[Send OTP Button]-->BackBtn[Back Button]
{{< /mermaid >}}

### Sign Up OTP Verification page
{{<mermaid align="left">}}
graph LR 
    ConfirmOtpBtn[Confirm OTP Button]-->ResendOtpBtn[RESEND OTP Button]
{{< /mermaid >}}

### Sign Up Success page
{{<mermaid align="left">}}
graph LR 
    SignUpSuccessOKBtn[OK Button]
{{< /mermaid >}}



### state machine
{{<mermaid align="center">}}
flowchart TD
    SignInPage((Sign in Page ))
	SignUpBtn[Sign Up Button]
	SignUpInfoPage[Sign Up Guide Page]
	GetStartedBtn[Get Started Button]
	SignUpFromPage[Sign Up Form Page]
	SignUpNextBtn[Next Button]
	UserConfirmationPage[UserConfirmation Page]
	SendOTPBtn[SEND OTP Button]
	OTPVerificationPage[OTP Verification Page]
	OTPConfirmBtn[Confirm Button]
	OTPResendBtn[RESEND OTP Button]
	ReceiveOTPS[Receive SMS OTP & Email OTP]
	NOOtps[NO SMS OTP & Email OTP]
	SignUpSuccessPage[SignUp Success Page]
	SignUpSuccessOKBtn[OK button]
	LoginPage[Login Page]
	
	SignInPage--C-->SignUpBtn
	linkStyle 0 stroke:blue,stroke-width:2px,color:black;
	SignUpBtn--S-->SignUpInfoPage
	linkStyle 1 stroke:green,stroke-width:2px,color:black;
	SignUpBtn--F-->SignInPage
	linkStyle 2 stroke:red,stroke-width:2px,color:black;
	SignUpInfoPage--C-->GetStartedBtn
	linkStyle 3 stroke:blue,stroke-width:2px,color:black;
	GetStartedBtn--S-->SignUpFromPage
	linkStyle 4 stroke:green,stroke-width:2px,color:black;
	GetStartedBtn--F-->SignUpInfoPage
	linkStyle 5 stroke:red,stroke-width:2px,color:black;
	SignUpFromPage--C-->SignUpNextBtn
	linkStyle 6 stroke:blue,stroke-width:2px,color:black;
	SignUpNextBtn--S-->UserConfirmationPage
	linkStyle 7 stroke:green,stroke-width:2px,color:black;
	SignUpNextBtn--F-->SignUpFromPage
	linkStyle 8 stroke:red,stroke-width:2px,color:black;
	UserConfirmationPage--C-->SendOTPBtn
	linkStyle 9 stroke:blue,stroke-width:2px,color:black;
	SendOTPBtn--S-->OTPVerificationPage
	linkStyle 10 stroke:green,stroke-width:2px,color:black;
	SendOTPBtn--F-->UserConfirmationPage
	linkStyle 11 stroke:red,stroke-width:2px,color:black;
	OTPVerificationPage--C-->OTPConfirmBtn
	linkStyle 12 stroke:blue,stroke-width:2px,color:black;
	OTPConfirmBtn--S-->SignUpSuccessPage
	linkStyle 13 stroke:green,stroke-width:2px,color:black;
	OTPConfirmBtn--F-->OTPVerificationPage
	linkStyle 14 stroke:red,stroke-width:2px,color:black;
	SignUpSuccessPage--C-->SignUpSuccessOKBtn
	linkStyle 15 stroke:blue,stroke-width:2px,color:black;
	SignUpSuccessOKBtn--S-->LoginPage
	linkStyle 16 stroke:green,stroke-width:2px,color:black;
	SignUpSuccessOKBtn--F-->SignUpSuccessPage
	linkStyle 17 stroke:red,stroke-width:2px,color:black;
	OTPVerificationPage--C-->OTPResendBtn
	linkStyle 18 stroke:blue,stroke-width:2px,color:black;
	OTPResendBtn--S-->ReceiveOTPS
	linkStyle 19 stroke:green,stroke-width:2px,color:black;
	OTPResendBtn--F-->NOOtps
	linkStyle 20 stroke:red,stroke-width:2px,color:black;
	ReceiveOTPS--C-->OTPConfirmBtn
	linkStyle 21 stroke:blue,stroke-width:2px,color:black;
	
		
{{< /mermaid >}}

| Symbol| Description|
|--|--|
| C| OnClick|
| S| OnSuccess|
| F| OnFailure|


### Flowchart : User Sign Up Flow
{{<mermaid align="center">}}
%%{init: {'themeVariables': {'edgeLabelBackground':'#FFFF', 'tertiaryColor': '#fff0f0'}}}%%

flowchart TD
    Start((start ))
    subgraph Initial Look
    SetSignUpInitialLook[Set Up Sign Up From Initial Look & get phone Number using ConfigureUtils and set to field]
    GetHostNameFromDB[Get HostName From DB]
    RouteDataCheck{RouteData}
    PutHostNameAndCompanyListInPrefHelp[Put HostName and companyList in Pref Helper]
    MethodCallInvokeRouteAuthorization[Method Call: invokeRouteAuthorization]
    end
    
    subgraph Method: invokeRouteAuthorization
    InternetConnection1{Internet Connection}
    ShowMessageNetInfo>Please Connect With Internet]
    OnResponse1{Response}
    APICallInvokeToGetDomain{API Call : invokeRouteAuth}
    ShowMessageExceptionDailong>show Message: Exception Alert Dialog]
    ShowMessageApiConnectionError>show Message: Api Connection Error]
    MethodCallInvokeToGetDomain[Method Call: invokeToGetDomain]
    end
    
    subgraph Method: invokeToGetDomain
    InternetConnection2{Internet Connection}
    ShowMessageNetInfo2>Please Connect With Internet]
    OnResponse2{Response}
    APICallgetStagingHostname{API Call : getStagingHostname}
    ShowMessageExceptionDailong2>show Message: Exception Alert Dialog]
    ShowMessageApiConnectionError2>show Message: Api Connection Error]
    MethodCallpersistInLocalDB[Method Call : persistInLocalDB]
    MethodCallRoutingLogout[Method Call : routingLogout]
    end
    
    subgraph Method: persistInLocalDB
    getRouteDataFromDB[Database Call: get RouteDataObject]
    RouteDataOject{RouteData Object}
    InsertRouteData[Database call: insert RouteDataObject]
    UpdateRouteData[Database call: update RouteDataObject]
    end
    
    subgraph Method: routingLogout
    InternetConnection3{Internet Connection}
    ShowMessageNetInfo3>Please Connect With Internet]
    OnResponse3{Response}
    APICallRoutingLogout{API Call : routingLogout}
    showMessageRoutingLogout>Log Message: Routing Logout Successfully]
    HideLoading>CommonUtils.hideLoading]  
    end 
    
    subgraph Sign Up Form
    SignUpFormPage[Sign Up Form Page]
    CheckValidation{Check Validation}
    ShowMessageInvalidData>show Message: Please Enter Valid data]
    MethodCallRegisterUser[Method Call: registerUser]
    end
    
    subgraph Method: registerUser
    ObjectPreparation[registerUser object creation]
    UserConfirmationDetailsPage[USer Conformation Details page]
    GetRegisterUSerInstace[Get RegisterUser Instace from Intent]
    RegisterUserobject{RegisterUser Object}
    SetUpConfirmationPage[Set Up Confirmation Page with values from RegisterUser object]
    MethodCallInvokeRouteAuthorization2[Method Call: invokeRouteAuthorization]
    end
 
    subgraph Method: invokeRouteAuthorization 2
    InternetConnection4{Internet Connection}
    ShowMessageNetInfo4>Please Connect With Internet]
    OnResponse4{Response}
    APICallInvokeRegisterAuth{API Call : invokeRegisterAuth}
    ShowMessageApiConnectionError4>show Message: Api Connection Error]
    MethodCallInvokeContext[Method Call: invokeContext]
    end   
    
    subgraph Method: Method: invokeContext
    InternetConnection5{Internet Connection}
    ShowMessageNetInfo5>Please Connect With Internet]
    OnResponse5{Response}
    APICallGetContext{API Call : getContext}
    ShowMessageExceptionDailong3>Show Message: Exception Alert Dialog]
    ShowMessageApiConnectionError5>show Message: Api Connection Error]
    MethodCallInvokeRegisterAPI[Method Call: invokeRegisterAPI]
    end     
    
    subgraph Method: Method: invokeRegisterAPI
    InternetConnection6{Internet Connection}
    ShowMessageNetInfo6>Please Connect With Internet]
    OnResponse6{Response}
    APICallISurveyUser{API Call : surveyUser}
    ShowMessageExceptionDailong4>Show Message: Exception Alert Dialog]
    ShowMessageApiConnectionError6>show Message: Api Connection Error]
    OTPVerificationPage[OTP Verification Page]
    end   
    
    subgraph OTP Verification Page 
    OtpFillCheck{OTP Fill Check}
    MethodCallInvokeValidateOtp[Method Call: invokeValidateOtp]
    end

    subgraph Method: invokeValidateOtp
    InternetConnection7{Internet Connection}
    ShowMessageNetInfo7>Please Connect With Internet]
    OnResponse7{Response}
    APICallIPushOtpData{API Call : pushOtpData}
    
    ShowMessageApiConnectionError7>show Message: Api Connection Error]
    FailedToken{Failed Token}
    FailedTokenEqualCheck{ Failed Token == UNSUCCESS_TOKEN }
    LoginPage[Navigate to Login Page]
    MethodCallInvokeRouteAuthorization3[Method Call: invokeRouteAuthorization]
        subgraph Signup Succes Page
        APICallSignUpUserLogout{API Call : signUpUserLogout}
        OnResponse10{Response}
        FinalSuccessLoginPage[Login Page]
        ShowMessageApiConnectionError10>show Message: Api Connection Error]
        end
    end 
    
    

    subgraph Method: invokeRouteAuthorization3
    InternetConnection8{Internet Connection}
    ShowMessageNetInfo8>Please Connect With Internet]
    OnResponse8{Response}
    APICallIInvokeRegisterAuth{API Call : invokeRegisterAuth}
    ShowMessageApiConnectionError8>show Message: Api Connection Error]
    MethodCallInvokeContext2[Method Call: invokeContext]   
    end    
    
    subgraph Method: Method: invokeContext
    InternetConnection9{Internet Connection}
    ShowMessageNetInfo9>Please Connect With Internet]
    OnResponse9{Response}
    APICallGetContext2{API Call : getContext}
    ShowMessageApiConnectionError9>show Message: Api Connection Error]
    RepeatMethodCallInvokeValidateOtp[Repeat From InvokeValidateOtp Method Call]  
    end   
    End((end)) 
    
    %%connections start
    Start-->SetSignUpInitialLook
    SetSignUpInitialLook-->GetHostNameFromDB
    GetHostNameFromDB-->RouteDataCheck
    RouteDataCheck--Not NULL-->PutHostNameAndCompanyListInPrefHelp
    RouteDataCheck--NULL-->MethodCallInvokeRouteAuthorization
    
    MethodCallInvokeRouteAuthorization-->InternetConnection1
    InternetConnection1--Connected-->APICallInvokeToGetDomain
    InternetConnection1--Not Connected-->ShowMessageNetInfo
    APICallInvokeToGetDomain--OnResponse-->OnResponse1
    OnResponse1-- != 200-->ShowMessageExceptionDailong
    APICallInvokeToGetDomain--OnFailure-->ShowMessageApiConnectionError
    OnResponse1-- == 200-->MethodCallInvokeToGetDomain
    
    MethodCallInvokeToGetDomain-->InternetConnection2
    InternetConnection2--Connected-->APICallgetStagingHostname
    InternetConnection2--Not Connected-->ShowMessageNetInfo2
    APICallgetStagingHostname--OnResponse-->OnResponse2
    APICallgetStagingHostname--OnFailure-->ShowMessageApiConnectionError2
    
    OnResponse2-- != 200-->ShowMessageExceptionDailong2
    OnResponse2-- == 200-->MethodCallpersistInLocalDB
    MethodCallpersistInLocalDB-->getRouteDataFromDB
    getRouteDataFromDB-->RouteDataOject
    RouteDataOject--NULL-->InsertRouteData
    RouteDataOject--Not NULL-->UpdateRouteData
    InsertRouteData-->SignUpFormPage
    UpdateRouteData-->SignUpFormPage
    
    OnResponse2-- == 200-->MethodCallRoutingLogout
    MethodCallRoutingLogout-->InternetConnection3
    InternetConnection3--Connected-->APICallRoutingLogout
    InternetConnection3--Not Connected-->ShowMessageNetInfo3
    APICallRoutingLogout--OnResponse-->OnResponse3
    OnResponse3-- == 200-->showMessageRoutingLogout 
    APICallRoutingLogout--OnFailure-->HideLoading
    
    SignUpFormPage--Input Required Data-->CheckValidation
    CheckValidation--true-->MethodCallRegisterUser
    CheckValidation--false-->ShowMessageInvalidData
    
    MethodCallRegisterUser-->ObjectPreparation
    ObjectPreparation-->UserConfirmationDetailsPage
    
    UserConfirmationDetailsPage-->GetRegisterUSerInstace
    GetRegisterUSerInstace-->RegisterUserobject
    RegisterUserobject--Not NULL-->SetUpConfirmationPage
    SetUpConfirmationPage-->MethodCallInvokeRouteAuthorization2
    
    MethodCallInvokeRouteAuthorization2-->InternetConnection4
    InternetConnection4--Connected-->APICallInvokeRegisterAuth
    InternetConnection4--Not Connected-->ShowMessageNetInfo4
    APICallInvokeRegisterAuth--OnResponse-->OnResponse4
    APICallInvokeRegisterAuth--OnFailure-->ShowMessageApiConnectionError4
    OnResponse4-- == 200-->MethodCallInvokeContext    
    
    MethodCallInvokeContext-->InternetConnection5
    InternetConnection5--Connected-->APICallGetContext
    InternetConnection5--Not Connected-->ShowMessageNetInfo5
    APICallGetContext--OnResponse-->OnResponse5
    APICallGetContext--OnFailure-->ShowMessageApiConnectionError5
    OnResponse5-- == 200-->MethodCallInvokeRegisterAPI 
    OnResponse5-- != 200-->ShowMessageExceptionDailong3
    
    MethodCallInvokeRegisterAPI-->InternetConnection6
    InternetConnection6--Connected-->APICallISurveyUser
    InternetConnection6--Not Connected-->ShowMessageNetInfo6
    APICallISurveyUser--OnResponse-->OnResponse6
    APICallISurveyUser--OnFailure-->ShowMessageApiConnectionError6
    OnResponse6-- == 200-->OTPVerificationPage
    OnResponse6-- otherwise-->ShowMessageExceptionDailong4    
   
    OTPVerificationPage--Click Continur Button-->OtpFillCheck
    OtpFillCheck--filled-->MethodCallInvokeValidateOtp
    
    MethodCallInvokeValidateOtp-->InternetConnection7
    InternetConnection7--Connected-->APICallIPushOtpData
    InternetConnection7--Not Connected-->ShowMessageNetInfo7
    APICallIPushOtpData--OnResponse-->OnResponse7
    APICallIPushOtpData--OnFailure-->ShowMessageApiConnectionError7
    OnResponse7-- == 200--> APICallSignUpUserLogout
    OnResponse7-- == 401-->FailedToken 
    FailedToken-->FailedTokenEqualCheck
    FailedTokenEqualCheck--Equal-->LoginPage
    FailedTokenEqualCheck--Not Equal-->MethodCallInvokeRouteAuthorization3
    
    APICallSignUpUserLogout--OnResponse-->OnResponse10
    APICallSignUpUserLogout--OnFailure-->ShowMessageApiConnectionError10
    OnResponse10-- == 200-->FinalSuccessLoginPage

    FinalSuccessLoginPage-->End
    
    MethodCallInvokeRouteAuthorization3-->InternetConnection8
    InternetConnection8--Connected-->APICallIInvokeRegisterAuth
    InternetConnection8--Not Connected-->ShowMessageNetInfo8
    APICallIInvokeRegisterAuth--OnResponse-->OnResponse8
    APICallIInvokeRegisterAuth--OnFailure-->ShowMessageApiConnectionError8
    OnResponse8-- == 200-->MethodCallInvokeContext2
    
    MethodCallInvokeContext2-->InternetConnection9
    InternetConnection9--Connected-->APICallGetContext2
    InternetConnection9--Not Connected-->ShowMessageNetInfo9
    APICallGetContext2--OnResponse-->OnResponse9
    APICallGetContext2--OnFailure-->ShowMessageApiConnectionError9
    OnResponse9-- == 200-->RepeatMethodCallInvokeValidateOtp    
      
    
{{< /mermaid >}}

    

### Sequence Diagram :
#### [Routing API](http://localhost:1313/productspecification/features/mobileapplication/api/routing-api/)  

{{<mermaid align="center">}}
sequenceDiagram
	participant Login as Login
	participant KVDB as KV Database
	participant SQLite as SQLite Database
    participant SignUp as Sign Up Module
    participant Net as Network Utils
    participant cloud as GS-Cloud
    autonumber
    
    rect rgb(244,244,244)
        SignUp->>+SQLite: get RouteHostname
        SQLite-->>-SignUp: RouteData Object  
        Note right of SignUp: If RouteData == NULL { refer Routing API } else { go to step ( 3 ) }  
    end       
    
    rect rgb(244,244,244)
        SignUp->>+KVDB: get RegisterUser
        KVDB-->>-SignUp: RegisterUser Object    
    end 
    
    rect rgb(244,244,244)
        Note right of SignUp: If Hostname ! = NULL
        SignUp->>+Net: Check Internet , POST /api/login invokeRegisterAuth
        Net--x-SignUp: F : Connection Error
        SignUp->>+cloud: S : POST /api/login invokeRegisterAuth
        cloud-->>-SignUp: RES 200    
    end
    
    rect rgb(244,244,244)
        SignUp->>+Net: Check Internet , GET /api/1/CtxDto GetContext
        Net--x-SignUp: F : Connection Error
        SignUp->>+cloud: S : GET /api/1/CtxDto GetContext
        cloud-->>-SignUp: RES 200    
    end    

    rect rgb(244,244,244)
        SignUp->>+Net: Check Internet , PUT "/api/1/SurveyUser surveyUser"
        Net--x-SignUp: F : Connection Error
        SignUp->>+cloud: S : PUT "/api/1/SurveyUser surveyUser"
        cloud-->>-SignUp: RES 200    
    end 
    
    rect rgb(244,244,244)
        SignUp->>+Net: Check Internet , POST "/api/1/SurveyUserOtp pushOtpData"
        Net--x-SignUp: F : Connection Error
        SignUp->>+cloud: S : POST "/api/1/SurveyUserOtp pushOtpData"
        cloud-->>-SignUp: RES 200 {go to step 24 }
        SignUp->>+cloud: S : POST "/api/1/SurveyUserOtp pushOtpData"
        cloud-->>-SignUp: RES 401 {go to step 23 }
    end      
    
    rect rgb(244,244,244)
            Note right of SignUp: from step 22 failedToken = response.headers().get(ApiUtils.JWT_AUTH)
            Note right of SignUp: if (failedToken != null) { if(unsuccessful.equals("unsuccessful"){go to step 23 }} else { go to step 5 }
            SignUp->>Login: navigate to Login Page
    end  

    rect rgb(244,244,244)
        SignUp->>+Net: Check Internet , signUpUserLogout
        Net--x-SignUp: F : Connection Error
        SignUp->>+cloud: S : GET https://{hostname}/api/logout signUpUserLogout
        cloud-->>-SignUp: RES 200
    end

    rect rgb(244,244,244)
        SignUp->>Login: Sign Up Success  
    end    
        
   
        
          
{{< /mermaid >}}


[comment]: <> (### Request and Response JSON Data: based on operation number)

[comment]: <> (#### **Payload RouteData Object :**)

[comment]: <> (Route Data Object From Local Database)

[comment]: <> (        {)

[comment]: <> (            "expiryTime":1608196803034,)

[comment]: <> (            "hostnameApd":"ts.gramsevak.gov9.in",)

[comment]: <> (            "hostnameApi":"ts.gramsevak.gov9.in",)

[comment]: <> (            "hostnameApp":"ts.gramsevak.gov9.in",)

[comment]: <> (            "id":"4ff26169-7ed5-4064-a1ad-71eeea676168",)

[comment]: <> (            "state":"qats",)

[comment]: <> (            "surveyCompanyList":"[ Shadkona Tech Pvt Ltd, ApptoneLabs Tech Pvt Ltd ]")

[comment]: <> (        })

        

[comment]: <> (#### **Payload POST /api/invokeRouteAuth invokeRouteAuthentication :**)

[comment]: <> (Request sent : Anonymous user          )
        
[comment]: <> (        {)

[comment]: <> (            "password":"39ae086a-8cab-40b5-93ef-7ec6905b6aa4",)

[comment]: <> (            "username":"39ae086a-8cab-40b5-93ef-7ec6905b6aa4#@@#ebSCwqhJrSxF5z/ZYGEVKdo3WIw2uYCDsxXucSDzCD76ZVMcgsz/oqpw1RK3YAIfrQQ4vnFOIMDykpKqOivbvA==")

[comment]: <> (        })
       
[comment]: <> (Response: authToken   )
        
[comment]: <> (        authToken : Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzUxMiJ9.eyJpc3MiOiJzZWN1cmUtYXBpIiwiYXVkIjoic2VjdXJlLWFwcCIsInN1YiI6I)

[comment]: <> (                    jM4MTQ4NDIxLWFmZGItNDMwNy1hYTA1LTExN2QzMTJkN2RlZiIsImV4cCI6MTYwODQ1NjAwMSwicm9sIjpbIlJPTEVfQURNSU4iLCJST0x)

[comment]: <> (                    FX1NDT1BFX1NUQVRFIl19.c71kaQUeaeGURnS5YB-M6EAwo51UsyPjVWMedCBUdAQgI7ep-4TTeOco7A-wFx4Iu83sl4a2fJI3rvIcoOeVqg)
        
        
[comment]: <> (#### **Payload GET /api/1/Route/qats getStagingHostname :**)

[comment]: <> (Response :)
        
[comment]: <> (        {)

[comment]: <> (            "state":"qats",)

[comment]: <> (            "hostnameMap":{ )

[comment]: <> (                            "app":"ts.gramsevak.gov9.in",)

[comment]: <> (                            "apd":"ts.gramsevak.gov9.in",)

[comment]: <> (                            "api":"ts.gramsevak.gov9.in")

[comment]: <> (                          },)

[comment]: <> (            "surveyCompanyList":["Shadkona Tech Pvt Ltd","ApptoneLabs Tech Pvt Ltd"],)

[comment]: <> (            "expiryTime":1608198685842})

[comment]: <> (#### **Payload persistInLocalDB&#40;RouteData routeData&#41; :**)

[comment]: <> (Insert or Update Route Data object in Local Database)

[comment]: <> (    {"state":"qats","hostnameMap":{"app":"ts.gramsevak.gov9.in","apd":"ts.gramsevak.gov9.in","api":"ts.gramsevak.gov9.in"},"surveyCompanyList":["Shadkona Tech Pvt Ltd","ApptoneLabs Tech Pvt Ltd"],"expiryTime":1608198685842})

[comment]: <> (#### **Payload Fetching RegisterUser From KV Database.**)

[comment]: <> (####  **Payload POST /api/auth invokeRegisterAuth**)

[comment]: <> (#### **Payload GET /api/getContext GetContext**)

[comment]: <> (#### **Payload POST /api/surveyUser surveyUser**)

[comment]: <> (### **Payload POST /api/1/SurveyUserOtp pushOtpData**)


## Security compliance check
1. The only user having valid Aadhaar Details, PhoneNumber, and Email Addresses should Sign Up in the application.

## Operational Enablement
1. Nothing specific use case found

## Deprecation functionality
1. Nothing specific use case found

## User Manual
1.

## Feature/Defect list
| Feature/Defect ID | Link                                                     | Status |
|-------------------|----------------------------------------------------------|--------|
| GS-0002           | [GS-0002](https://shadkona.atlassian.net/browse/GS-0002) | Closed |


## References
1. [Android Developer Docs](https://developer.android.com/docs)

## Development Estimations
| Release Tag | Feature/Defect ID | Scrum Details   | Start date  | End date    |
|-------------|-------------------|-----------------|-------------|-------------|
| 2020OCT     | GS-0002           | Scrum 2020OCTs2 | 14 OCT 2020 | 28 OCT 2020 |

## Feature Doneness Criteria
Check list for the Doneness criteria

| Metric                       | Unit Measure | Expected Result | Actual Result | Accepted? | Remarks               | Approver  |
|------------------------------|--------------|-----------------|---------------|-----------|-----------------------|-----------|
| Acceptance Criteria Defined? | YES or NO    | YES             | YES           | Accepted  | All test cases passed | PM        |
| Architecture Approved?       | YES or NO    | YES             | YES           | Accepted  | Design is accepted    | Architect |
| Coding Completed?            | YES or NO    | YES             | YES           | Completed | Completed             | EM        |
| Product Defects              | Number       | 0               | 0             | Accepted  || EM                    |
| Unit Test Case Count?        | Number       | >5              | 8             | Accepted  | Tested                | EM        |
| Integration Test Cases Count | Number       | >5              | 9             | Accepted  | Tested                | EM        |
| Sonar Vulnerabilities Count  | Number       | 0               | 0             | Accepted  | validated             | EM        |
| Code Coverage                | Number       | >98%            | 99%           | Accepted  | Validated             | EM        |
| User Manual Verified?        | YES or NO    | YES             | YES           | Accepted  | Validated             | DocM      |
| PenTest Defect Count?        | Number       | <2              | 0             | Accepted  | Validated             | EM        |
| PM Accepted?                 | YES or NO    | YES             | YES           | Accepted  | Good to go            | PM        |
| OM Accepted?                 | YES or NO    | YES             | YES           | Accepted  | Good to go            | OM        |
| Deployed to Staging?         | YES or NO    | YES             | YES           | Accepted  | Good to go            | EM        |
| Deployed to Production?      | YES or NO    | YES             | YES           | Accepted  | Good to go            | OM        |
