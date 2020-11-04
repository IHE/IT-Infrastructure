**Integrating the Healthcare Enterprise**

![IHE\_LOGO\_for\_tf-docs](media/IHE-logo.jpeg)

**IHE ITI**

**Technical Framework Supplement**

**Internet User Authorization (IUA)** with updates to MHD and ATNA.

**Trial Implementation**

Date: October 29, 2020

Author: ITI Technical Committee

Email: iti@ihe.net

**Please verify you have the most recent version of this document.** See [here](http://ihe.net/Technical_Frameworks/) for Trial Implementation and Final Text versions and [here](http://ihe.net/Public_Comment/) for Public Comment versions.

**Foreword**

This is a supplement to the IHE IT Infrastructure Technical Framework V17.0. Each supplement undergoes a process of public comment and trial implementation before being incorporated into the volumes of the Technical Frameworks.

This supplement is published on October 30, 2020 for trial implementation and may be available for testing at subsequent IHE Connectathons. The supplement may be amended based on the results of testing. Following successful testing it will be incorporated into the IT Infrastructure Technical Framework. Comments are invited and may be submitted at [http://www.ihe.net/ITI\_Public\_Comments](http://www.ihe.net/ITI_Public_Comments/).

This supplement describes changes to the existing technical framework documents.

"Boxed" instructions like the sample below indicate to the Volume Editor how to integrate the relevant section(s) into the relevant Technical Framework volume.

| **Editor please Amend Section X.X by the following:**  |
|--------------------------------------------------------|

Where the amendment adds text, make the added text **<ins>bold underline</ins>**. Where the amendment removes text, make the removed text **~~bold strikethrough~~**. When entire new sections are added, introduce with editor's instructions to "add new text" or similar, which for readability are not bolded or underlined.

General information about IHE can be found at: [http://www.ihe.net](http://www.ihe.net/).

Information about the IHE IT Infrastructure domain can be found at: [http://www.ihe.net/IHE\_Domains](http://www.ihe.net/IHE_Domains/).

Information about the structure of IHE Technical Frameworks and Supplements can be found at: [http://www.ihe.net/IHE\_Process](http://www.ihe.net/IHE_Process/) and [http://www.ihe.net/Profiles](http://www.ihe.net/Profiles/).

The current version of the IHE Technical Framework can be found at: [http://www.ihe.net/Technical\_Frameworks](http://www.ihe.net/Technical_Frameworks/).

**CONTENTS**

<!-- TOC depthFrom:1 depthTo:2 -->

- [Introduction to this Supplement](#introduction-to-this-supplement)
- [Open Issues and Question](#open-issues-and-question)
- [Closed Issues](#closed-issues)
- [General Introduction](#general-introduction)
- [Volume 1 -- Profiles](#volume-1----profiles)
- [34 IUA Profile](#34-iua-profile)
    - [34.1 IUA Actors, Transactions, and Content Modules](#341-iua-actors-transactions-and-content-modules)
    - [34.2 IUA Actor Options](#342-iua-actor-options)
    - [34.3 IUA Required Actor Groupings](#343-iua-required-actor-groupings)
    - [34.4 IUA Overview](#344-iua-overview)
    - [34.5 IUA Security Considerations](#345-iua-security-considerations)
    - [34.6 IUA Cross Profile Considerations](#346-iua-cross-profile-considerations)
- [Volume 2 -- Transactions](#volume-2----transactions)
    - [3.71 Get Authorization Token](#371-get-authorization-token)
    - [3.72 Incorporate Authorization Token](#372-incorporate-authorization-token)
    - [3.102 Introspect Token](#3102-introspect-token)
    - [3.103 Get Authorization Server Metadata](#3103-get-authorization-server-metadata)
- [33 MHD Profile](#33-mhd-profile)

<!-- /TOC -->

# Introduction to this Supplement

### Problem Statement

This profile is motivated by customer requirements for authorizing network transactions, when using HTTP RESTful transports. IHE has authorization profiles for the Web Services and SOAP based transactions. This profile provides an authorization profile for the HTTP RESTful transactions.

Being authorized means that the user, patient or provider, has legitimate access to this HTTP RESTful service. The authorization includes identifying the user and the application that is making the request to the HTTP RESTful server, so that server can make further access control decisions.

The HTTP RESTful transport is being used by many healthcare applications and smart devices. These share a common set of issues. A typical use case example is:

-   The patient has a tablet and installs an application onto that tablet.

-   An application will need to retrieve and update health related data that is stored on a Resource Server. It uses HTTP RESTful transactions for both retrieve and update because HTTP support is integrated into the platform services.

-   Patients want to configure the application to have access to their data without needing the IT staff at the application vendor and resource vendor to set things up.

The HTTP RESTful services may include user driven browser activity, downloaded applications, and automatic devices. The existing IHE ITI XUA Profile fills these needs for the SOAP transport based transactions. The existing IHE ITI EUA Profile fills these needs for various different transports within a single enterprise environment, including HTTP RESTful transports.

The Basic Patient Privacy Consent (BPPC) Profile is associated with this profile and these other existing profile. BPPC covers the legal and administrative needs for consent documentation and associating the patient consent with policy documentation. The BPPC profile includes the ability to associate the electronic authorizations with the patient agreements and organizational policies.

It is important to understand that IUA is not a substitute for the administrative activities (such as withdrawing consent), policy setting, and other activities that BPPC documents provide. Greater integration of this authorization with third party authorization and consent documentation profiles, such as those found in the IHE BPPC Profile, are a future effort. This profile starts with just the basic authorization activities.

The administrative actions needed to establish an Authorization Server for IUA is not covered by these profile. These activities depend upon the operational needs, organizational and privacy policies that apply to a particular deployment.

### Background on the problem environment

The application interacts with both patient and Authorization Server to support the granting of an access token. The application then uses the access token to retrieve and update health related data.

The key issues here are:

-   Reliable and accurate authorization decisions, as part of an overall privacy protecting and security environment.

-   Application developers expect one common method for obtaining and using access tokens.

-   Resource Servers expect one common method for receiving access tokens as part of HTTP RESTful transactions, and one common method for processing these tokens.

-   Users, patients and providers, expect to be in control, do not want to depend on support staff to set up their applications, and want to minimize the interference from authorization requirements.

Similar issues arise with:

-   In house application distribution that needs authorization for applications used within the facility.

-   IT administrators prefer a common method to authorize use of in house web applications and access to in house resources.

-   Providers and Specialists have authorization needs for dealing with other organizations and need to deal with many resource services.

-   Granting subset access to specialized provider. E.g., read access to cardiac info to physical therapy organization, forbidding access to other sensitive health data.

There are also environmental assumptions made by this profile.

First, it is assumed that there will many systems working together to build the access control environment, where IUA provides one part only. For example, a glucose monitor may be authorized to have access to a patient's medical record. The expectation is that this will mean access to all of the glucose related information, which will include a variety of measurements and prescriptions. But, it is expected that if the device requests other sensitive health data about it will be rejected.

Second, this profile is operating in an environment where access consents are managed by BPPC or other mechanisms. IUA is not a substitute for documenting, establishing, and modifying these legal agreements. For example, there will be a documented consent agreement between a patient and a provider that the provider will provide medical records to a healthcare proxy that is identified and authorized by the patient. BPPC is one way to document that agreement.

# Open Issues and Question

- **Issue 11**: IUA does not define scopes at all, therefore IUA is not in conflict with SMART-on-FHIR. However this supplement includes updates to MHD and does define a Scope for use with MHD transactions. This definition today does not use SMART pattern, but does not forbid SMART scopes too. IHE requests comments on the IUA, MHD, and SMART-on-FHIR scope harmonization. 

- **Issue 12**: Given that the IUA Resource Server is grouped with some other IHE defined actor, and that actor has audit logging requirements; IUA does not need to give a defined audit event for success. IUA does impose adding an AuditEvent.entity to that audit even defined in the other profile. But this should be explained well enough for the reader to understand already. IHE requests comments on a need to define in IUA an AuditEvent specific to a Resource Server that is enforcing a DENY. This AuditEvent would be used when the Resource Server prevented the transaction from reaching the grouped Profile (e.g. MHD Document Responder). This AuditEvent would cover reasons for DENY that are thus not specific to the content of the grouped transaction. Reasons such as: Missing Token, Token validation failure, Token expiration, Scope mismatch, IUA required attributes missing, etc. The expectation is that we can leverage some codes from OAuth.
  
# Closed Issues

- **Issue 1**: At this time, the method for assignment of client identifiers is not included in the profile. Registration of clients is a significant operational and security problem that is being postponed until there is more experience with problems in the field and reasonable solutions. In the field there are a variety of methods being tried. Many depend upon physical distribution methods or out of band communications to manage the authentication problems.

- **Issue 2**: This profile does support access token in JWT format and SAML 2.0 Assertions compliant with the XUA profile requirements. An operational environment must ensure, that access tokens are understood by the authorization and Resource Servers. The Bearer Token option of earlier versions of the profile has been removed, since it does not specify the access token format and attributes used and was thus not interoperable by design.  

- **Issue 3**: Audit messages are only defined for clients that are also Secure Applications. There is no defined auditing for other clients.

- **Issue 4**: This profile does not require client grouping with Secure Node or Secure Application because it is using the OAuth client authentication methods. It assumes that the client authentication method will deal with security considerations in a manner similar to the certificate management assumptions made for TLS and other certificate users.

- **Issue 8**: This profile uses the Authorization header only for conveying the authorization information. The parameter form is not prohibited but is not compliant with the profile.

- **Issue 9**: This profile does not explain the ways that some Resource Servers utilize HTTP redirects to automate some kinds of authorization activities. The actual HTTP transactions used for Obtain Authorization Token and Authorized RESTful Transaction are as defined within this profile. The other transactions are under the control of the Resource Server and its design.

- **Issue 10**: The selected standards are: The OAuth 2.1 Framework, JWT Token, with defined extensions, SAML Token, using the XUA extensions.                 |


# General Introduction

| **Editor please Update the following Appendices to the General Introduction as indicated below. Note that these are not appendices to Volume but rather to the General Introduction.**  |
|------------------------------|

**Appendix A - Actor Summary Definitions**

| **Editor please Add the following actors to the IHE Technical Frameworks General Introduction list of actors:** |
|------------------------------|


|Actor                |Definition
|-----                |----------
|Authorization Client |A client that retrieve access tokens and presents them as part of transactions.
|Authorization Server |A server that issues access tokens to requesting clients.
|Resource Server      |A server that provides services that need authorization.


**Appendix B - Transaction Summary Definitions**

| **Editor please Add the following transactions to the IHE Technical Frameworks General Introduction list of Transactions:**  |
|------------------------------|


|Transaction                                |Definition
|-----------                                |----------
|Incorporate Authorization Token \[ITI-72\] |Add an access token to a transaction.
|Get Authorization Token \[ITI-71\]         |A transaction that is used to request and obtain an access token for use in Authorized transactions.
|Introspect Token \[ITI-102\]               |A transaction that is used to obtain the state and claims associated with an access token.
|Get Authorization Server Metadata \[ITI-103\]               |A transaction that is used to obtain metadata about a Authorization Server such as endpoint locations and signing key material


# Volume 1 -- Profiles

|  **Editor please add the following section 34 to Volume 1** |
|------------------------------|

# 34 IUA Profile

The IUA Profile adds authorization information to HTTP RESTful transactions. The IUA actors and behavior will be added to other profiles and transactions that need authorization.

## 34.1 IUA Actors, Transactions, and Content Modules

The actors in the IUA Profile manage the tokens used for authorization of access to HTTP RESTful services based on the flows and transactions defined in the OAuth 2.1 Authorization Framework [OAuth 2.1]. Authorization Clients interact with the Authorization Server to retrieve access tokens and incorporate them into HTTP RESTful transactions to authorize access to resources on the Resource Servers.

The OAuth 2.1 Authorization Framework requires client identification, which may be based on a *client\_id* parameter [OAuth 2.1, Section 2.2]. Depending on the grant type, the use of the *client\_id* MAY be required. For example the *Authorization Code* grant type requires the use of the *client\_id* for client identification [OAuth 2.1, Section 4.1], while the *Client Credential* grant type does not [OAuth 2.1, Section 4.2].

The OAuth 2.1 Authorization Framework also requires client authentication for confidential and credential clients [OAuth 2.1, Section 2.3]. It recommends the use of to use asymmetric (public-key based) methods for client authentication [OAuth 2.1, Section 9.1], but allows other suitable HTTP based authentication schemes matching the security policy of the Authorization Server [OAuth 2.1, Section 2.3.2].

This profile requires the use of a *client_id* for client identification and a *client_secret* used with the HTTP Basic Authentication scheme for client authentication of confidential and credentialed clients, if no other methods for identification and authentication are used.  

Depending on the grant type, the OAuth 2.1 Framework also requires user authentication. For example, the *Authorization Code* grant type covered by this profile requires user authentication [OAuth 2.1, Section 4.1], while the *Client Credential* grant type does not [OAuth 2.1, Section 4.2]. The methods used by the Authorization Server to authenticate the user (e.g., username and password login, session cookies, delegation to Authentication Server) is not scoped in the OAuth 2.1 Authorization Framework [OAuth 2.1, Section 3.1].

Since user authentication methods chosen depend on the projects or national security policy, they are not scoped in this profile and SHALL be defined in the specific implementation projects or national extensions of this profile. If the user authentication is not implemented in the Authorization Server, the use of OpenID Connect with the Authorization Grant or Hybrid flow is recommended.

It is the responsibility of the Resource Server to enforce the access policies based on the transaction performed and the information provided in the access token. Therefore the Resource Server MUST be able to rely upon the decisions made by the Authorization Server (e.g., client identification, user authentication), which requires that a trust relation between the Resource Server and the Authorization Server was established beforehand.  

The Resource Server MAY delegate the access policy enforcement to actors it is grouped with by providing the information from the access token and transaction data, or to other actors (e.g., by implementing the Authorization Decisions Verifier actor of the Secure Retrieve (SeR) supplement).

Note: An analogy of the segregation of duties for access control between the Authorization Server and the Resource Server is given in a  textbook (*Solving Identity Management in Modern Applications*, *APress 2019* by Yvonne Wilson and Abhishek Hingnikar) comparing the authorization and policy enforcement with a ticketing and entrance control to events (e.g, opera, cinema). In this analogy the Authorization Server provides the ticket which authorizes participation, while additional checks are performed to finally participate to the event.  

This profile relies on the OAuth 2.1 Authorization Framework. Since the original publication of OAuth 2.0 in 2012, several new RFCs have been published that add or remove functionality from the core specification. Version 2.1 of the OAuth Authorization Framework consolidates and simplifies the most commonly used features and best practices of OAuth 2.0.

![IUA Actor Diagram](media/1.2_IUA-actor-diagram.png)

Figure 34.1-1: IUA Actor Diagram

Table 34.1-1 lists the transactions for each actor directly involved in the IUA Profile. To claim compliance with this profile, an actor SHALL support all required transactions (labeled "R") and MAY support the optional transactions (labeled "O").

Table 34.1-1: IUA Profile - Actors and Transactions

|Actors               |Transactions                      |Optionality	|Reference      
|----                 |----                              |---        	|-----          
|Authorization Client |Incorporate Authorization Token   |R          	|Section 3.72
|                     |Get Authorization Token           |O          	|Section 3.71
|                     |Get Authorization Server Metadata |O           |Section 3.103
|Authorization Server |Get Authorization Token           |R          	|Section 3.71
|                     |Introspect Token                  |C  Note 1  	|Section 3.102
|                     |Get Authorization Server Metadata |O           |Section 3.103
|Resource Server      |Incorporate Authorization Token   |R          	|Section 3.72
|                     |Get Authorization Token           |C  Note 1   |Section 3.71
|                     |Introspect Token                  |C  Note 1  	|Section 3.102
|                     |Get Authorization Server Metadata |O           |Section 3.103

*Note 1:* Mandatory when the Token Introspection Option is declared.

### 34.1.1 Actor Descriptions and Actor Profile Requirements

The IUA actors are expected to be grouped with other actors that perform HTTP RESTful transactions. Grouping an Authorization Client with another actor means that this other actor will provide an access token as part of the HTTP transaction to a HTTP RESTful server. It MAY perform the Get Authorization Token transaction to obtain the access token. The corresponding HTTP RESTful server SHOULD be grouped with the Resource Server actor to indicate that the server can perform access control.

#### 34.1.1.1 Authorization Client

The Authorization Client performs the network transactions and user interactions needed to obtain an access token and to attach that token to transactions to indicate that the transactions are authorized. An Authorization Client in IUA supports the following associated transactions:

-   Get Authorization Server Metadata: In this case the Authorization Client interacts with the Authorization Server to obtain configuration metadata required for the further authorization steps such as Authorization endpoint locations and supported authorization grant types.

-   Get Authorization Token: In this case, the Authorization Client interacts with an Authorization Server to obtain a token that indicates HTTP RESTful transactions for a particular kind of service and device are authorized by the user. This MAY include interactions with the user for authentication purposes.

-   Incorporate Authorization Token: In this case the access token has already been obtained and is communicated as part of the HTTP RESTful transaction for some other profile or service. With this token the Authorization Client indicates that the HTTP RESTful transaction has been authorized by the Authorization Server. The Resource Server will validate the client's token with associated claims and enforce configured access policies before serving the request.

-   When the Incorporate Authorization Token is to be used with a FHIR server, an Authorization Client SHOULD query the [capabilities](http://hl7.org/fhir/R4/http.html#capabilities) endpoint on the Resource Server to determine if the Resource Server supports IUA. The element [**CapabilityStatement.rest.security.service**](http://hl7.org/fhir/R4/capabilitystatement.html) will be populated with the code "IUA" at system canonical URL "http://profiles.ihe.net/fhir/ihe.securityTypes/CodeSystem/securityTypes".

#### 34.1.1.2 Authorization Server

The Authorization Server provides access tokens to requesting clients. In IUA, the Authorization Server uses an authenticated user identity, the requested HTTP RESTful service URL to the Resource Server, and/or other information to determine whether HTTP RESTful transactions are authorized. If authorized, the Authorization Server provides an access token which authorizes the client to retrieve data and documents from the Resource Server.  

Authorization Servers declaring the Authorization Server Metadata option SHALL provide a metadata endpoint that provides configuration information to Authorization Client and Resource Servers. This information includes endpoint locations, supported authentication grants and signing key materials. This information greatly simplifies the configuration of those Authorization Clients and Resource Servers.

Authorization Servers declaring the Token Introspection option SHALL provide an endpoint usable by Resource Servers to validate and evaluate the access token. With this option, the Authorization Server MAY provide other token formats than JWT or SAML. Using this option, the token can be treated as an opaque data construct for Resource Servers. When Token Introspection option is used the Authorization Server SHALL provide the ITI-102 Token Introspection transaction service.


#### 34.1.1.3 Resource Server

The Resource Server provides services to access protected resources that need authorization. In IUA the Resource Server accepts a HTTP RESTful transaction request with an incorporated access token. It evaluates the access token to verify that the Authorization Server has authorized the transaction. The Resource Server MUST enforce this authorization and MAY perform additional authorization decisions that are specific to the requested service. The Resource Server MAY then allow the transaction to proceed, subject to access control constraints that MAY also be in place.

Resource Servers declaring the Authorization Server Metadata option SHALL have the means to be configured by interacting with an Authorization Server metadata endpoint. The obtained configuration information includes endpoint locations, token format, and signing key materials. This information simplifies the configuration of a Resource Server by allowing the majority of this information to be requested from an Authorization Server.

The Resource Server declaring the Token Introspection option SHALL have the ability to use the Token Introspection transaction to obtain the details of the token from the Authorization Server. This transaction can be used by the Resource Server when it is uncertain about the format of the token (JWT, SAML, or opaque), or when it wants to re-evaluate the authorization policy. To be able to invoke the introspection endpoint, the Resource Server MUST authenticate itself. It MAY obtain a access token of its own from the Authorization Server for this purpose.

Notes:

1. The Resource Servers and Authorization Servers MAY be grouped into an integrated product together with user authentication, access control, and other services.

2. In general, Resource Servers perform additional access control decisions and MAY restrict responses even for transactions authorized by the Authorization Server.

3. When the Incorporate Authorization Token is to be used with a FHIR server, Resource Server SHALL declare support for IUA in the [capabilities](http://hl7.org/fhir/R4/http.html#capabilities) endpoint using the element [**CapabilityStatement.rest.security.service**](http://hl7.org/fhir/R4/capabilitystatement.html) and the code "IUA" at system canonical URL "http://profiles.ihe.net/fhir/ihe.securityTypes/CodeSystem/securityTypes".


## 34.2 IUA Actor Options
Resource Server and Authorization Server actors SHALL support at least one of the following three options: the JSON Web Token option, the SAML Token option or the Token Introspection Option. The Authorization Client is not and does not need to be aware of the token processing options.

The **Authorization Server Metadata option** enables automated configuration of Resource Servers and Authorization Clients by enabling them to pull configuration metadata directly from the Authorization Server.

The **JWT Token Option** uses JSON Web Token encoding of the Token issued by the Authorization Server. The JSON Web Token constraints are defined in  [3.71.4.2.2 JSON Web Token Option](#371422-json-web-token-option)

The **SAML Token Option** enables integration of environments that use both, XUA compatible SAML access token and the OAuth authorization infrastructure. 

The **Token Introspection Option** uses the ITI-102 Token Introspection transaction to validate and obtain the claims associated with an access token. These are the same claims as described in [3.71.4.2.2 JSON Web Token Option](#371422-json-web-token-option). Introspection allows for custom token formats and re-evaluation of tokens after commission (enabling features like token revocation), at the cost of introspection calls to the Authorization Server.

Table 34.2-1: IUA - Actors and Options

| IUA Actor            | Option                        |Optionality
|----------------------|-------------------------------|----------
| Authorization Client | Authorization Server Metadata |O    		
| Authorization Server | JWT Token                     |O  Note 1  		
|                      | SAML Token                    |O  Note 1        
|                      | Token Introspection           |O  Note 1  		
|                      | Authorization Server Metadata |O    		
| Resource Server      | JWT Token                     |O  Note 1  		
|                      | SAML Token                    |O  Note 1  		
|                      | Token Introspection           |O  Note 1  		
|                      | Authorization Server Metadata |O

*Note 1:* Authorization Server or Resource Server actors MUST declare at least one of the following options: JWT Token, SAML, or Token Introspection.

## 34.3 IUA Required Actor Groupings

An actor from this profile SHALL implement the required transactions and/or content modules in this profile ***in addition to*** all of the transactions required for the grouped actor (Column 2).


Table 34.3-1: Required Actor Groupings


  |IUA Actor            |Actor to be grouped with   |Reference                    |Content Bindings Reference
  |----                 |-----                      |-----                        |-----                      
  |Authorization Server |Time Client                |ITI TF-1:7 Consistent Time   | --                          
  |Resource Server      |Time Client                |ITI TF-1:7 Consistent Time   | --                          
  |Authorization Client | --                        | --                          | --                          

## 34.4 IUA Overview

### 34.4.1 Concepts

The term "authorization" and "access control" are used colloquially for a variety of related activities. All of the concepts listed below are sometimes called "authorization" or "access control". See the IHE ITI Access Control white paper for a detailed discussion of Access Control concepts. This profile will use more specific terms for each of these activities. These are:

-   Provisioning -- Setting up the initial rules and updating them when the situation changes. The administrator may say "Authorize Dr. X to have access". The steps taken to make this happen are called provisioning.

-   Delegation -- Adding, transferring and revoking authorization from one person to another. This is closely related to provisioning. It differs in that it can only transfer authority that has already been provisioned, and it may track changes to provisioned access for the original person.

-   Authentication -- Determining that the actual user (at the moment of authentication) is the claimed identity.

-   Authorization -- Determining that the authenticated user is authorized to have access to a resource (at the moment of authorization). The profile describes how to convey authorization decisions. It is not defining how the decision is made.

-   Access Control -- A system of provisioning, delegation, authentication, and authorization. It is normal to have multiple nested levels of access control. This profile is concerned with whether access is allowed to make the HTTP transaction requests to the specified resources. There are likely also building access controls, Resource Server access controls, and other access controls involved.

#### 34.4.1.2 Terminology

This profile uses the terms "access token", "refresh token", "bearer token", "Authorization Server", "Resource Server", "authorization endpoint", "authorization request", "authorization response", "token endpoint", "grant type", "access token request", and "access token response" as defined by The OAuth 2.1 Authorization Framework [OAuth 2.1].

Additionally, this profile uses the terms "token introspection", "introspection endpoint", "introspection request", and "introspection response" as defined by the OAuth2 Token Introspection specification [RFC7662].

The OAuth 2.1 Authorization Framework uses the term "resource owner" for the user an authorized client may access data on behalf of. Typically in health related environments a healthcare professional access patients or organization related data (resources) for which the healthcare professional is not the "legal owner" but may access according to the access policies of the environment. To avoid any misunderstandings related to the OAuth term "resource owner" and the term "legal owner", this profile uses the term "user" instead.

In accordance with the definitions in the OAuth 2.1 Authorization Framework [OAuth 2.1] this profile distinguishes confidential clients, credentialed clients and public clients as follows:

- *confidential client* - a client which stores the client authentication data (e.g., client\_id and client\_secret) in a way, that the user has no access to it (e.g., a server hosted web application).

- *credentialed client* - a client which has credentials, but their identity has been not been confirmed by the Authorization Server.

- *public client* - a client where the user (in principle) has access to the client code and client data. Public clients cannot store client authentication data in a confidential way (e.g., single page web applications, native mobile apps on a device, if no additional features are implemented to make the client authentication data unavailable for the user).

*Note:* A public client classification does not automatically mean the client is insecure. Public clients typically are under the full control of the user (e.g., a native app on the users device) and secured against malicious attacks. Public clients just cannot hide authentication data from the user, making client authentication useless.

### 34.4.2 Use Cases

#### 34.4.2.1 Authorization

This profile applies to use cases where a user authorizes an client application to access health data on behalf of the user using OAuth. Beyond other, relevant use cases are:   

A healthcare professional uses a server hosted web application to access a patient's electronic health record (EHR) using RESTful transactions. The web application has been registered beforehand at the Authorization Server with client identifier and client authentication method (e.g. client secret) by a system administrator. When accessing a view on the EHR, the browser is redirected to the EHR Authorization Server. The Authorization Server authenticates the healthcare professional either by presenting the views to enter the authentication factors (e.g. username, password and 2nd factor) or by redirecting to an Identity Provider (IdP). This step may be omitted, if the browser already has an authenticated session (e.g. session cookie). After user authentication, the Authorization Server performs the necessary steps to authorize the web application access to the EHR data with application specific scope, either by contract or by explicit consent given by the healthcare professional. When authorized, the web application retrieves an access token which authorizes it to request and retrieve the EHR data from the Resource Server(s) with an application specific scope on behalf of the healthcare professional.

A healthcare professional uses a single page web application to access a patients electronic health record (EHR) using RESTful transactions. At initial startup the app registers with the Authorization Server using a dynamic client registration protocol. When accessing a view on the EHR, the steps follow the same steps as in the web application use case above.   

A clinical monitor managed by the hospital system administrators access a patients EHR using RESTful transactions in the hospital LAN. At installation time, clinical monitor has been registered at the Authorization Server with client identifier and client authentication method (e.g. client secret) by the system administrator and a contracts (policies) have been deposited at the Authorization Server and Resource Server(s) authorizing access to the EHR with application specific scope. Before accessing patient EHR data, the clinical monitor requests an access token from the Authorization Server (e.g. using the client credential grant type). The clinical monitor incorporates the access token to the RESTful transactions to access EHR data and documents stored in the EHR Resource Server(s) with an application specific scope.   

A patient uses a native app on her mobile device to access data from her electronic health record (EHR) using RESTful transactions via the Internet. At first startup the app registers with the Authorization Server using a dynamic client registration protocol. When accessing a view on the EHR, the native app is redirected to the EHR Authorization Server, which authenticates the patient either by presenting the views to enter the authentication factors (e.g. username, password and 2nd factor) or by delegating to an Identity Provider (IdP). After user authentication, the Authorization Server performs the necessary steps to authorize the native app to access to the EHR data with application specific scope by explicit user consent. When authorized, the native app retrieves an access token which authorizes the app to request and retrieve the EHR data from the Resource Server(s) with an application specific scope on behalf of the patient.

The limitation of the scope is common to all use cases and on of the key concepts of OAuth to ensure data privacy protection by user consent. While the need for restricting the scope might be less obvious for primary system applications, it is apparently for mobile or web applications which provide specific services for patients or healthcare professionals, e.g., for medication or vaccinations or other specific use cases. An Authorization Server therefore in general will present a form to the user to consent to an application specific and limited scope, e.g., to specific transactions, document types or classes or subject specific data the application is authorized to access.    


#### 34.4.2.2 Delegation

There are multiple reasons to perform delegations. These cases primarily involve patient delegation choices. Providers rarely have the authority to delegate. IT staff may use delegation as part of the support for autonomous devices.

Users may delegate authority to:

-   Advocates and proxies who are authorized by the patient to make decisions for the patient.

-   Organizations that are acting for the patient, such as a visiting nurse organization that is providing support to the patient.

Revocation of delegation needs to be clearly specified by policy. Revocation may be removal of rights because of swapping devices. Expiration, re-authorization, etc. also need to be covered. Revocation is not just a response to breaches and failures. Revocation is a normal response to changes in people, equipment, and relationships.

## 34.5 IUA Security Considerations

IUA uses OAuth 2.1 which contains references to security analyses. There are also a variety of analyses available in the public literature. This profile does not introduce new considerations to those analyses. We have not identified any new healthcare related issues.

For confidential clients this profiles requires client authentication using client\_id and client\_secret, if no other reliable client authentication method is used, and the client registration with a fixed redirect\_uri.

IUA does not address issues around issuing and revoking client\_ids. OAuth 2.1 relies upon the client\_id for client identification and authorization. OAuth 2.1 does not further define how client\_ids are managed.

Usually Authorization Server publish web forms where system administrators and users can apply for a client\_id. OAuth 2.1 defines a mechanism for dynamically registering clients with Authorization Servers, by defining a set of desired client metadata values to be made available to the Authorization Servers [OAuth 2.1, Section 2].  

The Authorization Server will have an administratively managed list of approved client\_ids for accepted clients. This list will be updated as new clients are approved or existing clients are removed. An access token will not be issued for unapproved clients. This assumes that the client\_id management will deal with these security considerations in a manner similar to the certificate management assumptions made for secure communication transactions.

The Authorization Server will typically have an administratively managed list of approved Resource Servers. The list of Resource Servers is used in access control decisions to determine if a client has access to a Resource Server. These access control decisions take place when an access token is created, are associated with the access token, and may be re-evaluated when an access token is introspected. Introspection is initiated by a Resource Server just prior to servicing a client request. Introspection can therefore can be used to signal token revocation, or provide Resource Server specific authorization results (such as a limited view on the authorized scopes). 
 

## 34.6 IUA Cross Profile Considerations

The XUA profile provides equivalent functionality for SOAP based transactions. Both profiles, XUA and IUA define a transaction to incorporate a token into transactions accessing protected data. Both profiles have much in common, but also some remarkable differences:

- The XUA profile names a transaction to retrieve an SAML 2 assertion for authorization (Get X-User Assertion), but does not specify it in detail, leaving the details to national extensions and project specific implementations. In contrast the IUA profiles specifies the analog Get Authorization Token [ITI-71] for OAuth 2.1 compliant access token.

- While the XUA profile relies on ATNA Node Authentication to authenticate the client (or client network node), IUA uses the mechanism defined in the OAuth 2.1 Authorization Framework to authenticate client applications.

- While XUA supports SAML 2 Assertions only, the IUA profile supports access token in JWT, SAML 2.0 Assertion or custom formats (in case the Introspect option is implemented).  

The SAML token option in IUA enables an Authorization Client to incorporate access token originally retrieved and issued from a XUA X-Assertion Provider and use it in the Incorporate Authorization Token [ITI-72] transaction, when accessing protected data from a Resource Server via RESTful transactions.   

# Volume 2 -- Transactions

| **Editor please Add Section 3.71**  |
|------------------------------|


## 3.71 Get Authorization Token

This transaction is used by Authorization Clients to obtain an OAuth 2.1 compliant access token for use in a RESTful transaction to access data from a Resource Server.

The OAuth 2.1 Authorization Framework [OAuth 2.1, Section 4] defines the following authorization grant types:

-   *Authorization Code Grant* [OAuth 2.1, Section 4.1]. This grant type is optimized for confidential clients who make use of User Agents (e.g., web browsers).

-   *Client Credentials Grant* [OAuth 2.1, Section 4.2]. This grant type is optimized for clients requesting access tokens using only its client credentials and is restricted to confidential clients (e.g., medical devices, back end applications).

The OAuth 2.1 Authorization Framework further defines extension points to implement extension grant types [OAuth 2.1, Section 4.3]. Three are mentioned here specifically:

- *Device Authorization* [RFC 8628]: This grant type is optimized for devices that cannot use a browser to perform a user-agent-based authorization or don’t provide interfaces for the user to input text required for authorization and authentication (e.g., medical devices, mobile health sensors).

- *SAML Client or User Assertions* [RFC 7522]: To use a SAML Assertion as a credential for client or user authentication, the Authorization Client SHALL perform the access token request in conformance with the *SAML 2.0 Profile for OAuth 2.0 Client Authentication and Authorization Grants*. This type of grant MAY be used to exchange a XUA Compliant SAML 2.0 assertion to a token format preferred by the Authorization Server.

- *JSON Web Token (JWT) grants* [RFC 7523]: To use a JWT Token as credential for client or user authentication, the Authorization Client SHALL perform the access token request in conformance with the *JSON Web Token (JWT) Profile for OAuth 2.0 Client Authentication and Authorization Grants*. This type of grant provides better security properties than the client credential flow as it allows for asymmetric keys to be used for client and user authentication. 

The SAML and JWT grants from RFC7522 and RFC7523 MAY be used in federation scenarios where an Authorization Server will accept tokens from another Authorization Server as credentials for issuing access tokens.

Both the RFC7522 and RFC7523 require the existence of a public key infrastructure. The operational aspects of such infrastructure are beyond the scope of this specification.

This profile is scoped to the *Authorization Code* and *Client Credential* grant types. To claim compliance with this profile, the Authorization Server SHALL support the *Authorization Code* and *Client Credential* grant type and MAY support the *Device Authorization*, *SAML Client or User Assertions*, *JSON Web Token (JWT) Grants* or other OAuth 2.1 extension grant types.   

### 3.71.1 Scope

This transaction SHALL be used by Authorization Clients to retrieve an OAuth 2.1 compliant access token defined in [Section 3.71.4.2 Get Authorization Token Response](#37142-get-authorization-token-response) of this profile.

### 3.71.2 Actor Roles

This profile defines the following actors and roles:

Table 3.71.2-1: Actor Roles

|Actor                  |Role                                                           |
|-------                |-----                                                          |
|Authorization Client   | Client requesting an access token to authorize RESTful transactions    |
|Resource Server        | Server requesting an access token to authorize token introspection requests    |
|Authorization Server   | Server that grants access tokens.                             |

*Note:* The requirements for the Authorization Client and Resource Server are identical for this transaction. For brevity, the solely term Authorization Client is used in the remainder of this transaction description. 

### 3.71.3 Referenced Standards

This transaction relies on standards defined in the following documents and the references therein:

- *OAuth 2.1*: The OAuth 2.1 Authorization Framework, published as draft-ietf-oauth-v2-1-00, July 30, 2020.

- *JWT Access Token*: JSON Web Token (JWT) Profile for OAuth 2.0 Access Tokens, published as draft-ietf-oauth-access-token-jwt-10, September 2020.

- *RFC 7519*: JSON Web Token (JWT), May 2015.  

- *RFC 7522*: Security Assertion Markup Language (SAML) 2.0 Profile for OAuth 2.0 Client Authentication and Authorization Grants, May 2015.

- *RFC 7515*: JSON Web Signature (JWS), May 2015.

- *RFC 7518*: JSON Web Algorithms (JWA), May 2015.

- *RFC 4648*: The Base16, Base32, and Base64 Data Encodings, October 2006

### 3.71.4 Messages

![ITI-71 Flow Diagram](media/basic-flow.png)

Figure 3.71.4-1: Basic Process of the Authorization Token Request and Incorporate Authorization Token transaction

```plantuml
@startuml basic-flow

group Get Authorization Server Metadata (ITI-103)
AuthorizationClient -> AuthorizationServer : Get Authorization Server Metadata
AuthorizationClient <-- AuthorizationServer : configuration metadata
end

group Get Authorization Token (ITI-71)
AuthorizationClient -> AuthorizationServer : Authorization Request
AuthorizationClient <-- AuthorizationServer : Authorization Response + Authorization Token
end

group Incorporate Authorization Token (ITI-72)
AuthorizationClient -> ResourceServer : Resource Request + Authorization Token
AuthorizationClient <-- ResourceServer : Resource Response
end

@enduml
```

Main Flow:

1.  (Optional) The Authorization Client fetches the metadata document from the Authorization Server to detect the relevant authorization endpoints and supported grant types.

2.  The Authorization Client authenticates to the Authorization Sever and (optionally) provides claims related to the intended request to access protected resources of the Resource Server.

3.  The Authorization Server authenticates the client, validates the claims against any policy rules (such as user consent) and generates an access token that authorizes the Authorization Client to request the protected resources from Resource Servers.

4. The Authorization Server incorporates the access token to the requests of the protected resources to Resource Servers.

5. The Resource Server evaluates the access token and the resource request and enforces the access policies. This MAY involve an additional token introspection request towards the Authorization Server if the Introspection Option is used.


#### 3.71.4.1 Get Authorization Token Request

The Get Authorization Token Request is performed by an Authorization Client or Resource Server (in case of the Introspect option) to obtain an access token to be used in further communication. The sequence of HTTP(S) requests to perform an Get Authorization Token transaction depends on the grant type (type of credentials) chosen.

This profile currently requires support for two types of grants:
* OAuth2 Client Credential grant
* Authorization Code grant

##### 3.71.4.1.1 Client Credential grant type

![ITI-71 Client Credential](media/client-credential-grant.png)

Figure 3.71.4.1.1-1: Sequence of HTTP requests in the client credential grant type.

```plantuml
@startuml client-credential-grant

participant "Authorization Client" as Client
participant "Authorization Server" as AuthzServer

autonumber 0 1 "<b>[00]</b>"

group Get Authorization Token (ITI-71) [Client Credentials Grant]
Client -> AuthzServer: Access Token Request
AuthzServer --> Client: Access Token Response
end

autonumber stop

@enduml
```

The Authorization Client requests an access token using client credentials (or other supported means of authentication). This grant type SHALL be used by confidential clients only [OAuth 2.1, Section 4.2].

The Authorization Client actor claiming the Authorization Server Metadata option SHALL use the *token_endpoint* URL from the Authorization Server Metadata Document to obtain the access token.

The Authorization Client makes a HTTP(s) POST request to the token endpoint with the following parameters in the HTTP request entity-body [OAuth 2.1, Section 4.2.2]:

- *grant_type* (REQUIRED): The value of the parameter SHALL be *client_credentials*.

- *resource* (OPTIONAL): Single valued identifier of the Resource Server api endpoint to be accessed [JWT Access Token, Section 3].

- *scope* (OPTIONAL): The scope claimed by the Authorization Client.

The request SHALL use the *application/x-www-form-urlencoded* format with a character encoding of UTF-8 [OAuth 2.1, Section 4.2.2].

The Authorization Clients SHALL present its client\_id and client\_secret in a HTTP Basic Authentication Header to the Authorization Server.

A non-normative example of the access token request with client authentication using the *client_id* and *client_secret* in the HTTP Authorization header, MAY be as follows:

```http
POST /token HTTP/1.1
Host: server.example.com
Authorization: Basic czZCaGRSa3F0MzpnWDFmQmF0M2JW
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials
&scope=scope_1 scope_2 ... scope_N
&resource=https://rs.example.com/
```

##### 3.71.4.1.2 Authorization Code grant type

![ITI-71 Authorization Code](media/authorization-code-grant.png)

Figure 3.71.4.1.1-1: Sequence of HTTP requests in the client authorization code grant type.

```plantuml
@startuml authorization-code-grant

actor User

participant "User Agent" as UserAgent
participant "Authorization Client" as Client
participant "Authorization Server" as AuthzServer

autonumber 0 1 "<b>[00]</b>"

group Get Authorization Token (ITI-71) [Authorization Code Grant]
Client -> UserAgent: Redirect to Authorization Server \n(authorization request incl requested scopes, resource, etc.)
UserAgent -> AuthzServer: authorization request

note over User, AuthzServer
  Authorization Server determines access based on
  user authentication, consent and/or other policies.
end note

AuthzServer -> UserAgent: Redirect to Client \n(authorization response with Authorization Code)
UserAgent -> Client: authorization response

Client -> AuthzServer: Token Request \n(client credentials + Authorization Code)
AuthzServer --> Client: Access Token Response (access token)
end

@enduml
```

This grant type SHALL be used by confidential, credential and public clients, if the explicit consent of the user is required to authorize the Authorization Client to access data on behalf of the user.

The Authorization Client actor claiming the Authorization Server Metadata option SHALL use the "authorization_endpoint" URL from the Authorization Server Metadata Document to redirect the User-Agent.

The Authorization Client directs the user-agent to make a HTTP GET request to the authorization endpoint with the following parameters using the "application/x-www-form-urlencoded" format [OAuth 2.1, Section 4.1.1.3]:

- *response_type* (REQUIRED): The value MUST be *code*.

- *client_id* (REQUIRED, IF KNOWN): The identifier the Authorization Client is registered at the Authorization Server.

- *state* (REQUIRED): An unguessable value used by the client to track the state between the authorization request and the callback to the redirect URI. While this parameter is optional in the OAuth 2.1 Authorization Framework [OAuth 2.1, Section 4.1.1.3] it is required in this profile for security reasons.

- *resource* (OPTIONAL): Single valued identifier of the Resource Server endpoint to be accessed [JWT Access Token, Section 3].

- *code_challenge* (REQUIRED): A challenge derived from the client generated code verifier used to correlate the authorization request to the token request [OAuth 2.1, Section 4.1.1 and references therein].

- *code_challenge_method* (OPTIONAL): Indicator used for the code challenge transformation method. It's value MAY be *plain* or *S256* [OAuth 2.1, Section 9.8].  

- *redirect_uri* (OPTIONAL): The absolute URI of the Authorization Client callback endpoint to which the Authorization Server will send the user agent back once access is granted (or denied). This parameter is required if the Authorization Client is registered at the Authorization Server with multiple redirect URI, optional otherwise [OAuth 2.1, Section 3.1.2.3].  

- *scope* (OPTIONAL): The scope claimed by the Authorization Client.

A non-normative example of the authorization request is as follows:

```http
GET /authorize?
  response_type=code
  &client\_id=s6BhdRkqt3
  &state=xyz
  &redirect_uri=https%3A%2F%2Fclient%2Eexample%2Ecom%2Fcb
  &code_challenge=6fdkQaPm51l13DSukcAH3Mdx7_ntecHYd1vi3n0hMZY
  &code_challenge_method=S256
  &resource=https%3A%2F%2Frs.example.com%2F
  &scope=scope_1%20scope_2%20scope_N
  HTTP/1.1
Host: server.example.com
```

If the access request is granted (by the user or some other access policy), the Authorization Server issues an authorization code. 

The Authorization Server SHALL redirect the user agent to the Authorization Clients redirect URI with the authorization response parameter in the *application/x-www-form-urlencoded* format. The response parameter SHALL be as follows:

- *code* (REQUIRED): The authorization code generated by the Authorization Server.  

- *state* (REQUIRED): An unguessable value used by the client to track the state between the authorization request and the callback.

```http
HTTP/1.1 302 Found
Location: https://client.example.com/cb?code=SplxlOBeZQQYbYS6WxSbIA&state=xyz
```

The Authorization Client SHALL use the *authorization code* in an access token request to retrieve an access token and token metadata from the Authorization Server.

The Authorization Client actor claiming the Authorization Server Metadata option SHALL use the "token_endpoint" URL from the Authorization Server Metadata Document to obtain the access token.

It makes a HTTP POST request to the token endpoint with the following parameters in the HTTP request entity-body [OAuth 2.1, Section 4.1.3]:   

- *grant_type* (REQUIRED): The value SHALL be "authorization_code".

- *code* (REQUIRED): The authorization code received from the Authorization Server in the authorization response.

- *redirect_uri* (REQUIRED): The redirect URI of the Authorization Client callback. The value SHALL match the redirect URI the Authorization Client is registered at the Authorization Server and the value of the *redirect_uri*, if presented in the authorization request.

- *client\_id* (REQUIRED): The client identifier the Authorization Client is registered with at the Authorization Server, if no other authentication scheme is used for client authentication.

- *code_verifier*: The original code verifier string. REQUIRED, if the "code_challenge" parameter was used in the authorization request. SHALL NOT be used otherwise.

A non-normative example of the access token request with client authentication using the *client\_id* and *client_secret* in the HTTP Authorization header, MAY be as follows:

```http
POST /token HTTP/1.1
Host: server.example.com
Authorization: Basic czZCaGRSa3F0MzpnWDFmQmF0M2JW
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code
&code=SplxlOBeZQQYbYS6WxSbIA
&redirect_uri=https%3A%2F%2Fclient%2Eexample%2Ecom%2Fcb
&code_verifier=3641a2d12d66101249cdf7a79c000c1f8c05d2aafcf14bf146497bed

```

##### 3.71.4.1.3 Expected Actions
The Authorization Server upon receiving a Get Token Request SHALL validate all incoming values, including (non-exhaustive):
* scope values
* client identifier and credentials
* resource values
* redirect uris
* authorization codes

The scope parameter incorporated in the token requests SHALL be used to restrict authorization grants to specific actions (e.g., restrict authorization to specific resources to read-only) and to convey claims, which at runtime are known to the Authorization Client only (e.g., if the user claims a breaking-the-glass access in a emergency situation). The Authorization Server MAY refuse token requests that mention scope values that are unknown to the Authorization Server.

Authorization Servers SHOULD limit the list of identifiers in the audience claim to a minimum to avoid token misuse by unintended parties.

The Authorization Client is RECOMMENDED to provide a resource value to limit usability of the requested token to the intended Resource Server. If provided, the Authorization Server SHOULD evaluate any resource values provided as part of the token request procedure. The Authorization Server SHOULD execute policies to detect wether the client has access to the indicated resource. If the Authorization Client presented a resource value in the token request, the Authorization Servers MUST limit the list of Resource Server identifiers in the audience claim to only those that are essential to interact with the specified resource (typically only the Resource Server itself).

If the request is valid, all access policy criteria are met the Authorization Server SHALL respond with the access token response as outlined in section [3.71.4.2 Get Authorization Token Response](#37142-get-authorization-token-response).

If the authorization request is invalid, the Authorization Server SHALL react as defined in [OAuth 2.1, Section 4.1.2.1].

###### 3.71.4.1.3.1 Client Credential grant type

The Authorization Server SHALL authenticate the Authorization Client using it's client identifier and secret as communicated in the HTTP Authorization header.

The Authorization Server SHALL verify the access token request as described in [OAuth 2.1, Section 4.2.2]

###### 3.71.4.1.3.2 Authorization Code grant type

The Authorization Server SHALL authenticate confidential and credential clients using the *client\_id* and *client\_secret*, or by other reliable client authentication method. In the latter case, the Authorization Server SHALL resolve the client authentication to a *client\_id* which was registered beforehand.     

The Authorization Server SHALL verify that all required parameters of the authorization request are present and valid. If valid, the Authorization Server SHALL authenticate the user and obtain the user consent (by presenting the user a form to authorize specific scopes or by establishing approval via other means). When the user consent is established, the Authorization Server SHALL issue an authorization code to the client redirect URI conveying the authorization code and client state value.

The Authorization Client SHALL use the authorization code to request the access token from the Authorization Server. The Authorization Server SHALL verify the access token request as described in [OAuth 2.1, Section 4.1.3]. 

#### 3.71.4.2 Get Authorization Token Response

##### 3.71.4.2.1 Message Semantics
The Authorization Server SHALL respond an error response as defined in the OAuth 2.1 Authorization Framework [OAuth 2.1, Section 5.2] if the request does not match the requirements or is not understood. 

If the access token request is valid and authorized, the Authorization Server responds the access token response message in JSON format with the following attributes [OAuth 2.1, Section 4.2.3]:

- *token_type* (REQUIRED): The value of the parameter SHALL be *Bearer*.

- *access_token* (REQUIRED): A JSON string containing the access token. The format of the access token string depends on the supported JWT Token, SAML Token or Introspect Token options.

- *scope* (REQUIRED): The scope granted by the Authorization Server.

- *expires_in* (OPTIONAL): This parameter MAY be used to inform the Authorization Client how long the access token is valid.  

- *refresh_token* (OPTIONAL): A token provided by the Authorization Server which can be used by the Authorization Client to obtain new access tokens using the same authorization grant.  

The access token response MAY contain other parameter or extensions depending on the implementation details of the Authorization Server [OAuth 2.1, Section 4.2.3].

The Authorization Server SHALL include the HTTP *Cache-Control* response header field with value *no-store* and the *Pragma* response header field value *no-cache* to the access token response [OAuth 2.1, Section 4.2.3].

A non-normative example of the access token response is as follows:

```http
HTTP/1.1 200 OK
Content-Type: application/json
Cache-Control: no-store
Pragma: no-cache
{
  "token_type": "Bearer",
  "access_token": "2YotnFZFEjr1zCsicMWpAA",
  "scope": "scope_1 scope_2 ... scope_M",
  "expires_in": 3600,
  "refresh_token": "tGzv3JOkF0XG5Qx2TlKWIA",
  "example_parameter": "example_value"
}
```

##### 3.71.4.2.2 JSON Web Token Option
The OAuth2 specifications does not indicate the structure of the access token. Actors conforming to the JSON Web Token Option SHALL support access tokens formatted as signed JWT Tokens.

JWT token SHALL be signed as specified in JSON Web Signature [RFC 7515]. If signed, the JWS Compact Serialization (base64 encoded, with single signature or MACed) SHALL be used as described in [RFC 7515, Section 7.1].

Any actor that supports this transaction MAY support the JWE (unsigned but encrypted) alternative of the JWT token.

Of the signature of JWT algorithms specified in the JSON Web Algorithms [RFC 7518], the following algorithm SHALL be supported:
- *HS256*: HMAC using SHA-256 hash algorithm.
- *RS256*: RSA using SHA-256 hash algorithm.

Other algorithms such as:
- *ES256*: ECDSA using P-256 curve and the SHA-256 hash algorithm ("ES256") are RECOMMENDED. Other algorithms MAY be supported except the "NONE" that MUST NOT be used.

*Note:* It is RECOMMENDED to use asymmetric (public-key based, e.g., RS256) methods for signing access token. When asymmetric methods are used, Resource Server do not need to store sensitive symmetric keys, making these methods more robust against malicious attacks.

In the JSON Web Token option the access token is defined as JSON object with the following attributes:

- *iss* (REQUIRED): A single valued string identifying the instance which issued the access token (e.g.,the Authorization Server) [JWT Access Token, Section 2.2].

- *sub* (REQUIRED): If known, unique identifier of the user; the *client\_id* otherwise [JWT Access Token, Section 2.2].  

- *client_id* (REQUIRED): identifier of the client for which the token is issued. [JWT Access Token, Section 2.2]

- *aud* (REQUIRED): An array of identifier strings for the Resource Server endpoints to be accessed [JWT Access Token, Section 2.2]. In the special case when the JWT has one audience, the "aud" value MAY be a single case-sensitive string.

- *jti* (REQUIRED): A unique identifier for the JWT access token [JWT Access Token, Section 2.2].

- *exp* (REQUIRED): Expiration time of the token in Numeric Date format [JWT Access Token, Section 2.2].

- *scope* (REQUIRED): The scope granted by the Authorization Server [JWT Access Token, Section 2.2.3].   

- *nbf* (OPTIONAL): The earliest time in Numeric Date format the token SHALL be accepted [JWT, Section 4.1.5].  

- *iat* (REQUIRED): The issuing date in Numeric Date format [JWT Access Token, Section 2.2].  

The JWT access token MAY contain other parameter or extensions depending on the implementation details.


###### 3.71.4.2.2.1 JWT IUA extension

The Authorization Server and Resource Server SHALL support the following extensions to the JWT access token:

- *subject\_name* (OPTIONAL): The user's name as String.

- *subject\_organization\_id* (OPTIONAL): Unique identifier of the user's organization. It's value SHOULD be an URI, i.e., an URL or an OID in URN notation.  

- *subject\_organization* (OPTIONAL): Name or description of the user's organization.

- *subject\_role* (OPTIONAL): Coded value indicating the user's role. If present, the value SHALL be formatted as FHIR Coding data type.   
- *purpose\_of\_use* (OPTIONAL): Purpose of use for the request. If a coded value is used, the value SHALL be formatted as FHIR Coding data type.   

- *home\_community\_id* (OPTIONAL): Home community identifier where the request originated. It's value SHOULD be an OID in URN notation.

- *national\_provider\_identifier* (OPTIONAL): A unique identifier issued to health care providers by their national authority.

- *person\_id* (OPTIONAL): Patient identifier, Citizen identifier, or other similar public identifier.

The above claims SHALL be wrapped in an "extensions" object with key 'ihe\_iua' and a JSON value object containing the claims, as such

```json
"extensions" : {  
  "ihe_iua" : {  
    "subject_name": "Dr. John Smith",
    "subject_organization": "Central Hospital",
    "subject_organization_id": "urn:oid:1.2.3.4",
    "other_value": "..."  
  }  
}
```

The claim content SHALL correspond to the content defined in the XUA specification (see ITI TF-2b: 3.40.4.1.2 Message Semantics).

The mapping of IUA extension claims to XUA compliant SAML 2.0 Assertion attributes is shown in Table 3.71.6.1.2-1 below.

Table 3.71.6.1.1-1: JWT claims of the IUA extension and corresponding XUA Assertion attributes

|JWT Claim                      |XUA Attribute              
|-------------------------------|---------------------------
|subject\_name                  |urn:oasis:names:tc:xspa:1.0:subject:subject-id
|subject\_organization          |urn:oasis:names:tc:xspa:1.0:subject:organization
|subject\_organization\_id      |urn:oasis:names:tc:xspa:1.0:subject:organization-id
|subject\_role                  |urn:oasis:names:tc:xacml:2.0:subject:role
|purpose\_of\_use               |urn:oasis:names:tc:xspa:1.0:subject:purposeofuse
|home\_community\_id            |urn:ihe:iti:xca:2010:homeCommunityId
|national\_provider\_identifier |urn:oasis:names:tc:xspa:1.0:subject:npi
|person\_id 					|*not defined*


###### 3.71.4.2.2.2 JWT BPPC extension

In an environment which uses the IHE BPPC profile for documenting the consent, the Authorization Server and Resource Server SHALL support the following extension parameter:

- *patient\_id*: Patient identifier related to the Patient Privacy Policy Identifier. It's value SHOULD be the patient identifier in CX syntax or as URL.

- *doc\_id*: Patient Privacy Policy Acknowledgment Document. It's value SHOULD be an URN or URL.

- *acp*: Patient Privacy Policy Identifier.

If present, the claims SHALL be wrapped in an "extensions" object with key 'ihe\_bppc' and a JSON value object containing the claims, as such

```json
"extensions" : {  
  "ihe_bppc" : {  
    "patient_id": "543797436^^^&amp;1.2.840.113619.6.197&amp;ISO",
    "doc_id": "urn:oid:1.2.3.xxx",
    "acp": "urn:oid:1.2.3.yyyy",
    "other_value": "..."    
  }  
}
```

The mapping of IUA extension claims to XUA compliant SAML 2.0 Assertion attributes is shown in table Table 3.71.6.1.2-1 below.  

Table 3.71.6.1.2-1: JWT claims of the BPPC extension and corresponding XUA Assertion attributes

|JWT Claim                      |XUA Attribute              
|-------------------------------|---------------------------
|patient\_id                    |urn:oasis:names:tc:xacml:2.0:resource:resource-id
|doc\_id                        |urn:ihe:iti:bppc:2007:docid
|acp                            |urn:ihe:iti:xua:2012:acp

###### 3.71.4.2.2.3 Example
The following is a non-normative example of JWT access token:

JOSE Header:
```json
{
"typ": "IUA-JWT",
"alg": "HS256"
}
```

JWS Payload:
```json
{
    "iss": "urn:tiani-spirit:sts",
    "sub": "b3ca1045-aa8b-42f9-9fd9-e0cbf5cb90a7",
    "aud": "http://ihe.connectathon.IUA/ResourceProvider-IHE-Connectathon",
    "exp": 1438251487,
    "nbf": 1438251187,
    "iat": 1438251187,
    "scope": "ITI-68",    
    "extensions" : {  
      "ihe_iua" : {  
        "subject_name": "Dr. John Smith",
        "subject_organization": "Central Hospital",
        "subject_organization_id": "urn:oid:1.2.3.4",
        "home_community_id": "urn:oid:1.2.3.4.5.6.7.8",
        "person_id": "urn:uuid:1.2.3.4",
        "subject_role": [
          {
            "system": "2.16.840.1.113883.6.96",
            "code": "46255001",
            "display": "Pharmacist"
          }
        ],
        "purpose_of_use": [
          {
            "system": "1.0.14265.1",
            "code": "12",
            "display": "Law Enforcement"
          }
        ]
      }
    }
}
```

##### 3.71.4.2.3 SAML Token Option
Authorization Servers implementing the SAML Token Options SHALL be able to format the access token as a SAML 2.0 assertion. 

The SAML 2.0 assertion content SHALL comply with XUA SAML assertion rules (see ITI TF-2b:3.40).

In accordance to [RFC7522, Section 2.2], the value of the access token contains a SAML 2.0 Assertion. It MUST NOT contain more than one SAML 2.0 Assertion. The SAML Assertion XML data MUST be encoded using base64url, where the encoding adheres to the definition in Section 5 of RFC4648 [RFC4648] and where the padding bits are set to zero. To avoid the need for subsequent encoding steps (by "application/x-www-form-urlencoded" [W3C.REC-html401-19991224], for example), the base64url-encoded data MUST NOT be line wrapped and pad characters ("=") MUST NOT be included.

##### 3.71.4.2.3 Token Introspection Option
Implementations relying on Token Introspection option are not restricted in the access token format. This format MAY be different from the JWT or SAML tokens as described in section [3.71.4.2.2](#371422-json-web-token-option) and [3.71.4.2.3](#371423-saml-token-option). 

*Note:* using this option, the access token MAY be formatted as an opaque identifier without further (security sensitive) content. In such cases, the Authorization Server MUST have means to retrieve and communicate the associated claims during token introspection (for details see transaction ITI-103)

### 3.71.5 Security Considerations

Authorization Client and Authorization Server claiming compliance with this profile SHALL fulfill the security requirements defined in the OAuth Authorization Framework [OAuth 2.1], especially:

- All HTTP transaction MUST be secured by using TLS or equivalent transport security.

- Authorization Clients SHALL verify the identity of the Authorization Server, either by validating the TLS certificate chain or by other reliable methods.

- Authorization codes SHALL be for single use and short-lived with a lifetime less or equal to 5 minutes.

- Access token SHOULD be short-lived with a lifetime of 1 hour or less. A lifetime less or equal to 5 minutes is RECOMMENDED.

- Refresh token MAY be long lived.

- To reduce the attack surface, client claims and authorization grants SHALL be the minimal. I.e., the authorization grant scope requested by the Authorization Client SHALL be the minimal required scope for the resource request to be used for.

#### 3.71.5.1 Security Audit Considerations

Authorization Servers SHOULD produce an audit record for any failed attempt to obtain authorization. IHE does not specify the format of audit records for Authorization Servers.

Authorization Clients MAY generate an audit message when an authorized transaction is performed or attempted.


|                                   | Field Name              | Opt             | Value Constraints|
|-----------------                  |-----------------        |-----------------|------------------|
| **Event**<br/>(AuditMessage/EventIdentification)                             | EventID                 | M               | EV(110114, DCM, "User Authentication") |
|                                   | EventActionCode         | M               | "E" (Execute)   |
|                                   | *EventDateTime*         | *M*             | *not specialized* |
|                                   | *EventOutcomeIndicator* | *M*             | *not specialized* |
|                                   | EventTypeCode           | M               | EV("ITI-71", IHE, "User Authorization")|
| **Source (1)**                    |                 |                 |                 |
| **Human Requestor (0)**           |                 |                 |                 |
| **Destination  (0)**              |                 |                 |                 |
| **Audit Source (Client Authentication  Agent) (1)** ||                |                 |                
| **Participant Object (1)**        |                 |                 |                 |

Where:

|                                   | Field Name              | Opt             | Value Constraints|
|-----------------                  |-----------------        |-----------------|------------------|
| **Source** <br/>(AuditMessage/ActiveParticipant) | UserID          | M               | The process ID as used within the local operating system in the local system logs.|
|                 | *Alternative UserID*  |  *U*       | *not specialized*            |
|                 | *UserName*      | *U*         | *not specialized*            |
|                 | *UserIsRequestor*  |  *M*         | *not specialized*           |
|                 | RoleIDCode      | M               | EV(110150, DCM, "Application")  |
|                 | NetworkAccessPointTypeCode  | M               | "1" for machine (DNS) name, "2" for IP address
|                 | NetworkAccessPointID  | M               | The machine name or IP address       |
| **Audit Source**<br/> AuditMessage/ AuditSourceIdentification    | *AuditSourceID* | *U* | *not specialized* |
|                                                             | *AuditEnterpriseSiteID* | *U* | *not specialized* |
|                                                             | *AuditSourceTypeCode*   | *U* | *not specialized* |
| **Token** <br/>(AuditMessage/ ParticipantObjectIdentification)  | ParticipantObjectTypeCode | M               | "2" (System)    |
|                 | ParticipantObjectTypeCodeRole | M               | "13" (Security Resource) |
|                 | *ParticipantObjectDataLifeCycle* | *U*         | *not specialized*            |
|                 | *ParticipantObjectIDTypeCode* | *U*         | *not specialized*           |
|                 | *ParticipantObjectSensitivity*  | *U*         | *not specialized*           |
|                 | *ParticipantObjectID*   | *U*         | *not specialized*            |
|                 | *ParticipantObjectName*  | *U*         | *not specialized*            |
|                 | ParticipantObjectQuery | M               | URL requested   |
|                 | *ParticipantObjectDetail* | *U*         | *not specialized*           |




| **Editor please Add Section 3.72**  |
|------------------------------|


## 3.72 Incorporate Authorization Token

### 3.72.1 Scope

This transaction is used to incorporate authorization information to HTTP RESTful transactions.


### 3.72.2 Actor Roles

Table 3.72.2-1: Actor Roles

|Actor                |Role
|------------         |-------------------------------------------------------------
| Authorization Client| Authorization component of a HTTP RESTful transaction client.
| Resource Server     | Authorization component of a HTTP RESTful transaction server.


### 3.72.3 Referenced Standards

This transaction relies on standards defined in the following documents and the references therein:

- *OAuth 2.1*: The OAuth 2.1 Authorization Framework, published as draft-ietf-oauth-v2-1-00. July 2020.

#### 3.72.3.1 Related IHE Profiles

XUA Cross-Enterprise User Assertion -- Attribute Extension

### 3.72.4 Interaction Diagram

![simple-iauth](media/incorporate-token.png)

Figure 3.72.4-1: Process flow for Incorporate Authorization Token
Transaction

```plantuml
@startuml incorporate-token

participant "Authorization Client" as client
participant "Resource Server" as rs
participant "Authorization Server" as as

group (optional) Get Authorization Server Metadata (ITI-103)
    rs -> as : Metadata request
    as --> rs: metadata
end

group Incorporate Authorization Token (ITI-72)

client -> rs : Resource Request + Access Token

alt JWT or SAML token
  rs -> rs: validate token

else introspect token
    rs -> as : Introspect Token (ITI-102)
    as --> rs: token claims
end

client <-- rs : Resource Response  
end  
@enduml
```

Main Flow:

1.  The Authorization Client sends a resource request to a Resource Server, together with the access token. The token is opaque to the Authorization Client

1. The Resource Server identifies the format of the token, validates the token, and obtains the claims associated with the token. To this end it MAY use the Authorization Server metadata, such as signing keys (for JWT or SAML tokens), or the introspect endpoint location.

1.  The Resource Server makes an access control decision based upon the information from the access token and the transaction details. It MAY provide access to the resource, a subset of the resource, or reject the request in total.

This transaction works in conjunction with other HTTP RESTful transaction. It extends the transaction by adding information to the HTTP request for that HTTP RESTful transaction.

### 3.72.5 Trigger Events

A client needs to make an HTTP RESTful transaction to a Resource Server that enforces access authorization.

### 3.72.6 Message Semantics

The Authorization Client SHALL incorporate the access token as received from the Authorization Server in a HTTP Authorization header of the type *Bearer* [OAuth2.1, Bearer token] as-is.

A non normative example of the access token incorporation to a RESTful transaction is as follows:

```http
GET /example/url/to/resource/location HTTP/1.1
Authorization: Bearer vGHTPOJzh3QFd\[...omitted for brevity...\]99bhgT8Ya
Host: example.com
```

### 3.72.7 Expected Actions
The Resource Server SHALL be able to determine the token format (JWT, SAML or other) through evaluating the "access_token_format" value in the Authorization Server Metadata document (see ITI-103), inspection of the access token value, or otherwise. When the Resource Server is not able to process the token format (through local verification or introspection) it MUST respond with HTTP 401 (Unauthorized).

The Resource Server SHALL validate or introspect the access token and ensure that it has not expired. 

If the token includes a scope claim, the Resource Server SHALL verify, that the scope covers the transaction to the requested resource [OAuth 2.1, Section 7].

If the token includes an audience claim, the Resource Server SHALL verify, that the audience includes the Resource Server itself [OAuth 2.1, Section 7].

The Resource Server SHALL verify, that the claims conveyed in the access token match the transaction type and data (E.g., verify that the patient_id attribute of the access token corresponds to the patient_id of the resource request).

In addition, the Resource Server SHALL enforce the access policies set in the specific environment by matching the information from the access token and the transaction data to the access policies.

If the token verification, scope matching or the access policy enforcement fails, the Resource Server SHALL respond a HTTP 401 (Unauthorized) error.

Authorization Clients receiving a HTTP 401 (Unauthorized) error SHOULD NOT retry the request with the same token. An Authorization Client SHOULD reformulate the request or obtain a new token from the Authorization Server before retrying.

#### 3.72.7.1 JSON Web Token Option
A Resource Server that claims conformance to the JSON Web Token Option SHALL be able to interpret and validate the access token as a JWT Token as defined in Section [3.71.4.2.2](#371422-json-web-token-option).

A Resource Server that claims conformance to the Authorization Server Metadata Option SHALL use the keys published through the Authorization Server Metadata Document for validating the JWT token's signature.

#### 3.72.7.3 SAML Token Option
A Resource Server that claims conformance to the SAML Token Option SHALL be able to interpret and validate the access token as a XUA compliant SAML Assertion as defined in Section [3.71.4.2.3](#371423-saml-token-option).

A Resource Server that claims conformance to the Authorization Server Metadata Option SHALL use the keys published through the Authorization Server Metadata Document for validating the SAML token's signature.

#### 3.72.7.4 Introspect Token Option
A Resource Server that claims conformance to the Token Introspection Option SHALL be able to interact with the Authorization Server using transaction ITI-102 as described in section [3.102](#3102-introspect-token) to validate the access token and obtain the related claims.

A Resource Server that claims conformance to the Authorization Server Metadata Option SHALL use the introspection endpoint published through the Authorization Server Metadata Document for validating the token and obtaining the related claims.

### 3.72.8 Security Considerations

Authorization Clients and Resource Servers claiming compliance with this profile SHALL fulfill the security requirements defined in the OAuth Authorization Framework [OAuth 2.1], especially:

- All HTTP transaction MUST be secured by using TLS or equivalent transport security.

- Authorization Clients SHALL verify the identity of the Resource Server when making requests to protected resources, either by validating the TLS certificate chain [OAuth 2.1, Section 7.4.2] or by other reliable methods.

#### 3.72.8.1 Security Audit Considerations

When an ATNA Audit message needs to be generated by the Resource Server and the user is authenticated by way of a JWT Token, the ATNA Audit message **UserName** element SHALL record the JWT Token information using the following encoding:

**alias\"\<\"user\"@\"issuer\"\>\"**

where:
-   **alias** SHALL match the JWT token's "aud" parameter
-   **user** SHALL match the JWT token's "sub" parameter
-   **issuer** SHALL match the JWT token's "iss" parameter

When an ATNA Audit message needs to be generated by the Resource Server and the user is authenticated by way of a SAML Token, the ATNA Audit message **UserName** element SHALL record the SAML token information using the following encoding:

**alias\"\<\"user\"@\"issuer\"\>\"**

where:
-   **alias** SHALL match the optional string within the SAML Assertion\'s Subject element SPProvidedID attribute
-   **user** SHALL match the required content of the SAML Assertion\'s Subject element
-   **issuer** SHALL match the X-Assertion Provider entity identifier contained with the content of SAML Assertion\'s Issuer element


| **Editor please Add Section 3.102** |
|------------------------------|


## 3.102 Introspect Token
Token introspection defines a protocol that allows Resource Servers to query the Authorization Server to determine the set of claims for a given token that was presented to them by an Authorization Client. These claims include whether or not the token is currently active and the authorization context in which the token was granted. 

Token introspection allows a Resource Server to query this information regardless of whether or not it is carried in the token itself (e.g. as encoded in a JWT token), allowing this method to be used along with or independently of structured token values. 

The Authorization Server MAY decide to mark an token as active or inactive based on internal policies executed during introspection. For example, a token MAY be marked inactive if it has expired, been revoked, or if the introspection requesting Resource Server is not part of the intended audience of the token. Note that the introspection response for inactive tokens do not contain other (privacy/security sensitive) claims, nor do they mention the reason why the token is marked inactive.

Additionally, token introspection is carried out in the context of a particular Resource Server, allowing the returned authorization claims to be tuned to that authorization context. For example, the Authorization Server MAY limit the list of scopes to those that are deemed relevant for the particular Resource Server.

### 3.102.1 Scope

This transaction SHALL be used by Resource Servers to request an OAuth2.1 compliant bearer token evaluation from an Authorization Server.

### 3.102.2 Actor Roles

This profile defines the following actors and roles:

Table 3.102.2-1: Actor Roles

|Actor                  |Role                                                           |
|-------                |-----                                                          |
|Resource Server        | Introspection Requester    |
|Authorization Server   | Introspection Responder    |

### 3.102.3 Referenced Standards

This transaction relies on standards defined in the following documents and the references therein: 

- *OAuth 2.1*: The OAuth 2.1 Authorization Framework, published as draft-ietf-oauth-v2-1-00, July 30, 2020.

- *RFC7662*: OAuth 2.0 Token Introspection, published as RFC7662, October 2015

### 3.102.4 Messages

The introspection option extends the message flow as depicted in the Incorporate Authorization Token message flow in section [3.72.4](#3724-interaction-diagram).

From the perspective of the Authorization Client there is no difference, but the Resource Server and Authorization Server engage in additional interactions to acquire and validate the token claims.

![ITI-102 Introspect Diagram](media/introspect.png)

Figure 3.102.4-1: ITI-102 Introspect Diagram

```plantuml
@startuml introspect 

participant "Authorization Client" as Client
participant "Resource Server" as ResourceServer
participant "Authorization Server" as AuthzServer

autonumber 0 1 "<b>[00]</b>"
autoactivate on

group (optional) Get Authorization Server Metadata (ITI-103)
    ResourceServer -> AuthzServer : Metadata request
    AuthzServer --> ResourceServer: metadata
end

group Get Authorization Token (ITI-71)
Client -> AuthzServer : Authorization Request  
Client <-- AuthzServer : Authorization Response\n(incl. Client Access Token)  

ResourceServer -> AuthzServer : Authorization Request  
ResourceServer <-- AuthzServer : Authorization Response\n(incl. Resource Server Access Token)  
end

group Incorporate Authorization Token (ITI-72)  
Client -> ResourceServer : Resource Request\n(incl. Client Access Token)

group Introspect Token (ITI-102)  
ResourceServer -> AuthzServer : Introspection Request\n(incl.Resource Server Access Token and Client Access Token)
ResourceServer <-- AuthzServer : Introspection Response
end

Client <-- ResourceServer : Resource Response  
end  

autonumber stop

@enduml
```

General flow:
* [00-01] Optionally, the Resource Server obtains a metadata document from the Authorization Server, providing the introspect endpoint location. 
* [02-05] The Authorization Client as well as the Resource Server independently obtain their access tokens from the Authorization Server. The Resource Server requires this token to invoke the introspection endpoint.
* [06] The Authorization Client will invoke a Resource Server endpoint embedding the access token in the request.
* [07-08] The Resource Server obtains the authorization claims associated with the token from the Authorization Server by invoking the introspect endpoint. This step MAY be omitted if the Resource Server has a cached introspect response value for the access token (including responses where the *active* field was set to false).
* [09] The Resource Server will evaluate the token claims, enforce any access control policies and return the requested resources to the Authorization Client.

#### 3.102.4.1 Token Introspection Request

The Resource Server Actor SHALL perform a HTTP POST request to the introspect endpoint with the following parameters using the "application/x-www-form-urlencoded" format [RFC7662]:

* *token (REQUIRED)* : The string value of the token. This is the Authorization Client's access\_token as received in the Authorization header in the request towards the Resource Server as defined in transaction ITI-72. 

A Resource Server stating conformance to the Authorization Server Metadata Option SHALL use the introspect endpoint as contained in the Authorization Server's metadata document.

The Token Introspection Request MUST be protected through TLS. 

The Resource Server MUST securely identify himself towards the Authorization Server by using credentials agreed between the Authorization Server and Resource Server. To this end, the introspect request is modelled as specialization of the ITI-72 transaction. This implies that the Resource Server MUST authenticate itself using a Bearer access token towards the Authorization Server. The Resource Server MAY obtain an access token from the Authorization Server using transaction ITI-71. 

*Note:* The use of bearer tokens to authorize the introspect request will not lead to circular references to introspect. The Authorization Server is expected to natively understand the bearer tokens it created and therefore does not need to call introspect on itself.

A non-normative example of an introspection request is (using a Bearer HTTP Authorization header), MAY be as follows:

```http
POST /introspect HTTP/1.1
Host: server.example.com
Authorization: Bearer 23410913-abewfq.123483
Accept: application/json
Content-Type: application/x-www-form-urlencoded

token=2YotnFZFEjr1zCsicMWpAA
```

##### 3.102.4.1.1 Trigger Events

Resource Server wishes to evaluate the validity and contents of an access token.

##### 3.102.4.1.2 Message Semantics

The token being introspected MAY be opaque to the Resource Server. It MAY be formatted as JWT or SAML token, but custom formats are allowed.

##### 3.102.4.1.3 Expected Actions

Upon receiving the introspect request, the Authorization Server MUST evaluate the Resource Server access to the introspect endpoint. In accordance to ITI-72, when access to the introspect endpoint is not allowed, the Authorization Server MUST return HTTP 401 (Not Authorized).

The Authorization Server SHALL:
* Validate the structure and authenticity of the token to be introspected
* Validate the active state of the token (e.g. check expiry or revocation)
* Evaluate configured access policies taking into account the authorization claims related to the token and the Resource Server identity
* formulate and return a introspect response

The Authorization Server MAY respond differently to different Resource Servers making the same request. For instance, an Authorization Server MAY limit which scopes from a given token are returned for each Resource Server to prevent a Resource Server from learning more about the larger network than is necessary for its operation.

The Authorization Server MAY include an expiry field (exp) in the introspect result. This expiry field value MUST be shorter or equal to the expiry time of the access token introspected.

#### 3.102.4.2 Token Introspection Response

Used to return the active state and authorization claims related to the token.

##### 3.102.4.2.1 Trigger Events

The Authorization has formulated an access policy decision for the introspected access token.

##### 3.102.4.2.2 Message Semantics

The introspect response is a JSON formatted object. There are two variants of this object.

1. The Authorization Server considers the token to be invalid for the given Resource Server because of formatting issues, revocation data, expiry or other access policy considerations. The introspect result object contains a single field "active" with boolean value "false".
2. The Authorization Server considers the token to be valid for the given Resource Server. The object will contain a field "active" with boolean value "true". In addition, it will contain the same fields and values as formulated for the JWT token content as specified in section [3.71.4.2.2 JSON Web Token](#371422-json-web-token-option), including defined extensions.

##### 3.102.4.2.3 Expected Actions

The Resource Server SHALL inspect the "active" field of the introspect result. In case the active field is set to "false" the Resource Server MUST return HTTP 401 (Not Authorized) for all requests carrying the introspected access token.

The Resource Server SHALL use the introspection results as access token claims in all access control evaluations as depicted in section [3.72.7](#3727-expected-actions).

The Resource Server MAY cache introspection results for a given access token in case the introspection result contains an expiry field. This cache MUST NOT extend the period as defined by the expiry field. In case no expiry field is provided, the introspection results MUST NOT be cached.

### 3.102.5 Security Considerations

Resource Server and Authorization Server claiming compliance with this option SHALL fulfill the security requirements defined in [RFC7662], especially

- All HTTP transaction MUST be secured by using TLS or equivalent transport security.

- Resource Servers SHALL verify the identity of the Authorization Server, either by validating the TLS certificate chain or by other reliable methods. 

- To avoid token leakage through query parameters, Resource Servers SHALL only use HTTP POST for the introspection request. HTTP GET is not specified, nor allowed by this profile.

- If the token can be used only at certain Resource Servers (as indicated by the resource field in the token request), the Authorization Server MUST determine whether or not the token can be used at the Resource Server making the introspection call.

- The Authorization Server MUST determine whether or not the token has expired.

- If the token can be revoked after it was issued, the Authorization Server MUST determine whether or not such a revocation has taken place.

- If the token has been signed (e.g. it is a JWT Token), the Authorization Server MUST validate the signature.

- To avoid disclosing the internal state of the Authorization Server, an introspection response for an inactive token SHOULD NOT contain any additional claims beyond the required "active" claim (with its value set to "false").

#### 3.102.5.1 Security Audit Considerations

Resource Servers SHALL use the introspection results as authorization claims when formulating audit messages, as specified in section [3.72.9](#3729-security-considerations).


| **Editor please Add Section 3.103** |
|------------------------------|

## 3.103 Get Authorization Server Metadata

This transaction is used by Authorization Clients and Resource Servers to obtain metadata about an Authorization Server such as endpoint locations and references to key stores required to validate (token) signatures.

### 3.103.1 Scope

This transaction is used by Authorization Clients and Resource Servers to obtain metadata about an Authorization Server such as endpoint locations and references to key stores required to validate (token) signatures.

### 3.103.2 Actor Roles

This profile defines the following actors and roles:

Table 3.103.2-1: Actor Roles

|Actor                  |Role                                                           |
|-------                |-----                                                          |
|Authorization Client   | Metadata Requester    |
|Resource Server        | Metadata Requester |
|Authorization Server   | Metadata Provider|

### 3.103.3 Referenced Standards

This transaction relies on standards defined in the following documents and the references therein: 

- *OAuth 2.1*: The OAuth 2.1 Authorization Framework, published as draft-ietf-oauth-v2-1-00, July 30, 2020.

- *RFC 8414*: OAuth 2.0 Authorization Server Metadata, June 2018

- *OpenID Connect Discovery*: OpenID Connect Discovery 1.0 incorporating errata set 1, November 2014

- *RFC 7517*:  JSON Web Key (JWK), May 2015


### 3.103.4 Messages
The Get Authorization Server Metadata transaction consists of a single request and response initiated by an Authorization Client or Resource Server as depicted in the diagram below:

![ITI-103 Get Authorization Server Metadata Diagram](media/get-authorization-server-metadata.png)

Figure 3.103.4-1: ITI-103 Get Authorization Server Metadata Diagram

```plantuml
@startuml get-authorization-server-metadata

participant "Authorization Client\nor\nResource Server" as Client
participant "Authorization Server" as AuthzServer

autonumber 0 1 "<b>[00]</b>"
autoactivate on

Client -> AuthzServer: Authorization Server Metadata Request
Client <-- AuthzServer: Authorization Server Metadata Response

@enduml
```

#### 3.103.4.1 Authorization Server Metadata Request

Used to request the metadata document of an Authorization Server

##### 3.103.4.1.1 Trigger Events

An Authorization Client or Resource Server wants to learn about Authorization Server endpoint locations, key material required for signature validation or other relevant authorization data.

##### 3.103.4.1.2 Message Semantics

The client issues a HTTP GET request to the well-known metadata endpoint associated with Authorization Server. 

There are various ways of formulating this endpoint as described in [RFC 8414, section 3.1], and [OpenID Connect Discovery, section 4]. Authorization Servers are RECOMMENDED to follow one of these procedures, but MAY choose a different well-known endpoint location mechanism.

A non-normative example of such a request using [RFC8414] MAY look like:

```http
GET /.well-known/oauth-authorization-server/tenant1 HTTP/1.1
Host: example.com
```

The manner in which the Authorization Clients or Resource Server are configured with the Authorization Server metadata endpoint locations is beyond the scope of this transaction.


##### 3.103.4.1.3 Expected Actions

Upon receiving a metadata request, the Authorization Server SHOULD respond with the metadata document as described in section [3.103.4.2](#310342-authorization-server-metadata-response). 

Implementations supporting multi-tenancy MUST respond with different metadata documents for different tenants, providing at least a different issuer value.

Requests for metadata for non-existing tenants MUST result in a HTTP 404 (not found) response.

#### 3.103.4.2 Authorization Server Metadata Response

The response is a set of claims about the Authorization Server's configuration, including all necessary endpoints and public key information.

##### 3.103.4.2.1 Trigger Events

The Authorization Server Metadata Response message is returned as response to a valid Authorization Server Metadata Request.

##### 3.103.4.2.2 Message Semantics

The response is a set of claims about the Authorization Server's configuration, including all necessary endpoints and public key location information.

The response MUST be structured as a plain JSON document.

The document MUST be structured according to the rules set forth in [RFC8414, Section 2], with the additional constraints:

* *issuer (REQUIRED)*: The Authorization Server's issuer identifier, which is a URL that uses the "https" scheme and has no query or fragment components. The URL MUST use the "https" scheme. The URL MUST contain the domain name of the URL at which the metadata document can be retrieved. The URL MUST contain any path elements referring to a tenant. Other path elements, such as those referring to the document location (e.g., ".well-known" or "openid-configuration") SHOULD be omitted. E.g., a valid issuer associated with a metadata document retrievable at `https://example.com/.well-known/oauth-authorization-server/tenant1` would be `https://example.com/tenant1`.
* *authorization_endpoint (REQUIRED)*: Authorization Server Authorization endpoint as used for the "authorization code" flow.
* *token_endpoint (REQUIRED)*: Authorization Server Authorization token endpoint location
* jwks_uri (CONDITIONAL). URL of the Authorization Server's JWK Set [RFC7517, Section 5] document. Authorization Server supporting the JWT Token or SAML token options MUST provide this claim to communicate the public keys that can be used to verify JWT token or SAML token signatures.
* *scopes_supported (OPTIONAL)*: The list of scopes supported by the Authorization Server. Note that IUA itself does not define the scopes of the transactions. Authorization Servers MAY opt to publish a subset of the scopes usable.
* *response_types_supported (REQUIRED)*: As the implicit grant flow is not supported in OAuth2.1, the response types SHOULD NOT include the value "token". Authorization Servers MUST include the response type "code". Authorization Servers supporting [OpenId Connect] or other standards MAY include other token types, such as "id_token".
* *grant_types_supported (REQUIRED)*: A JSON array listing the type of grants supported toward the token endpoint. The list MUST include the values "client_credentials", and "authorization_code". Authorization Servers supporting refresh tokens MUST include "refresh-token". Authorization Servers supporting the JWT grant MUST include "urn:ietf:params:oauth:grant-type:jwt-bearer". Authorization Servers supporting the SAML grant MUST include "urn:ietf:params:oauth:grant-type:saml2-bearer". Authorization Servers supporting other types of grants SHOULD provide additional values to this list representing those grant types.
* *token_endpoint_auth_methods_supported (OPTIONAL)*: JSON array containing a list of client authentication methods supported by this token endpoint. When provided, this list MUST include "client_secret_basic".
* *introspection_endpoint (CONDITIONAL)*: URL of the Authorization Server's OAuth 2.0 introspection endpoint. This claim MUST be provided by Authorization Servers supporting the Token Introspection Option.
* *introspection_endpoint_auth_methods_supported (CONDITIONAL)*: JSON array containing a list of client authentication methods supported by the introspection endpoint. This claim MUST be provided by Authorization Servers supporting the Token Introspection Option. As the introspect option mandates support for Resource Server bearer access tokens, this claim MUST include the "Bearer" value. Other authentication methods (e.g., "client_secret_basic") are allowed when supported by the Authorization Server.

In addition to the claims provided in [RFC8414] Authorization Servers SHOULD provide the following claim:

* *access_token_format (OPTIONAL)*:  JSON string defining the format of the access token as provided by the Authorization Server. This allows Resource Servers to learn about methods of verification. Authorization Server actors supporting the JWT Token option MUST set this claim value to "ihe-jwt". Authorization Server actors supporting the SAML Token Option MUST set this claim value to "ihe-saml". Authorization Servers providing tokens that are non-parsable MUST set this value to "opaque". Authorization Servers supporting access tokens in other structured formats MAY use alternative format identifiers.


##### 3.103.4.2.3 Expected Actions

The Authorization Client or Resource Servers requesting the metadata document SHALL use the endpoint locations from the metadata document in their interactions with the Authorization Server.

The Authorization Client or Resource Servers requesting the metadata document SHOULD use the JWK values retrieved from the jwks_uri endpoint published in the metadata document for validating JWT and/or SAML tokens.

Resource Servers requesting the metadata document SHOULD use the "access_token_format" claim to determine the method of token validation and usage (e.g. interpret and validate access token as JWT structure).

### 3.103.5 Security Considerations

All security considerations as described in [RFC8414, Section 6.2] MUST be implemented.

*Note:* The issuer claim value of the metadata document is not-necessarily the same as the issuer claim value associated with access-tokens. The issuer value in the metadata document refers to the source of the metadata document itself. This document MAY point to an token endpoint at a server other than the metadata document server. The issuer claim associated with the access token SHOULD refer to the server that implements the token endpoint.

As the metadata document is intended to support the authorization processes, there is no need to provide client credentials towards the metadata endpoint. To prevent unnecessary disclosure of credentials, the Authorization Server Metadata Request MUST NOT include and credentials from the Authorization Client or Resource Server.

| **Editor: Please add the following to MHD Volume 1: section 33.5 MHD Security Considerations**                      |
|------------------------------------------------|
# 33 MHD Profile

### 33.5.1 Use with IUA Profile

IUA profile provides support for user authentication, app authentication, and authorization decisions. When MHD actors are grouped with IUA actors there are additional security and privacy functionality enabled by this grouping. There are additional requirements and functionality enabled through scope definitions that are transaction specific. See the Security Considerations sections of the MHD defined transactions for guidance on scope definition when grouped with IUA actors.

| **Editor: Please add the following to MHD Volume 1: section 33.6 MHD Cross Profile Considerations**                      |
|------------------------------------------------|

### 33.6.4 Use with IUA Profile

IUA profile provides support for user authentication, app authentication, and authorization decisions. When MHD actors are grouped with IUA actors there are additional security and privacy functionality enabled by this grouping. There are additional requirements and functionality enabled through scope definitions that are transaction specific. See the Security Considerations sections of the MHD defined transactions for guidance on scope definition when grouped with IUA actors.

| **Editor: Please add the following to MHD Volume 2: section 3.65.5 Security Considerations**                      |
|------------------------------------------------|

#### 3.65.5.2 Use with IUA Profile

IUA profile provides support for user authentication, app authentication, and authorization decisions. When MHD actors are grouped with IUA actors there are additional security and privacy functionality enabled by this grouping. There are additional requirements and functionality enabled through scope definitions that are transaction specific.

An MHD Document Source when grouped with an IUA Authorization Client, SHALL request [ITI-71] the following scope from the IUA Authorization Server to enable the MHD [ITI-65] transaction authorizing token [ITI-72].  The MHD Document Responder when grouped with an IUA Resource Server SHALL require [ITI-72] Incorporate Authorization Token in all [ITI-65] Provide Document Bundle, SHALL enforce the authorization decision in the token, and MAY further enforce policies beyond those made by the Authorization Server such as consent or business rules.

scope: "ITI-65"

This scope request authorizes the full ITI-65 transaction. This scope implicitly requests patient specific Create/Update for DocumentManifest, DocumentReference, List, and Binary. Further scope refinement is allowed in realm or project specific situations, these additional scopes would be in addition to the scope defined here. 

| **Editor: Please add the following to MHD Volume 2: section 3.66.5 Security Considerations**                      |
|------------------------------------------------|

#### 3.66.5.2 Use with IUA Profile

IUA profile provides support for user authentication, app authentication, and authorization decisions. When MHD actors are grouped with IUA actors there are additional security and privacy functionality enabled by this grouping. There are additional requirements and functionality enabled through scope definitions that are transaction specific.

An MHD Document Consumer when grouped with an IUA Authorization Client, SHALL request [ITI-71] the following scope from the IUA Authorization Server to enable the MHD [ITI-66] transaction authorizing token [ITI-72]. The MHD Document Responder when grouped with an IUA Resource Server SHALL require [ITI-72] Incorporate Authorization Token in all [ITI-66] Find Document Manifests requests, SHALL enforce the authorization decision in the token, and MAY further enforce policies beyond those made by the Authorization Server such as consent or business rules. 

scope: "ITI-66"

This scope request authorizes the full [ITI-66] transaction. This scope implicitly requests patient specific Search/Read for DocumentManifest resources as defined in [ITI-66]. Further scope refinement is allowed in realm or project specific situations, these additional scopes would be in addition to the scope defined here. 

| **Editor: Please add the following to MHD Volume 2: section 3.67.5 Security Considerations**                      |
|------------------------------------------------|

#### 3.67.5.2 Use with IUA Profile

IUA profile provides support for user authentication, app authentication, and authorization decisions. When MHD actors are grouped with IUA actors there are additional security and privacy functionality enabled by this grouping. There are additional requirements and functionality enabled through scope definitions that are transaction specific.

An MHD Document Consumer when grouped with an IUA Authorization Client, SHALL request [ITI-71] the following scope from the IUA Authorization Server to enable the MHD [ITI-67] transaction authorizing token [ITI-72]. The MHD Document Responder when grouped with an IUA Resource Server SHALL require [ITI-72] Incorporate Authorization Token in all [ITI-67] Find Document References requests, SHALL enforce the authorization decision in the token, and MAY further enforce policies beyond those made by the Authorization Server such as consent or business rules. 

scope: "ITI-67"

This scope request authorizes the full [ITI-67] transaction. This scope implicitly requests patient specific Search/Read for DocumentReference resources as defined in [ITI-67]. Further scope refinement is allowed in realm or project specific situations, these additional scopes would be in addition to the scope defined here. 

| **Editor: Please add the following to MHD Volume 2: section 3.68.5 Security Considerations**                      |
|------------------------------------------------|

#### 3.68.5.2 Use with IUA Profile

IUA profile provides support for user authentication, app authentication, and authorization decisions. When MHD actors are grouped with IUA actors there are additional security and privacy functionality enabled by this grouping. There are additional requirements and functionality enabled through scope definitions that are transaction specific.

An MHD Document Consumer when grouped with an IUA Authorization Client, SHALL request [ITI-71] the following scope from the IUA Authorization Server to enable the MHD [ITI-68] transaction authorizing token [ITI-72]. The MHD Document Responder when grouped with an IUA Resource Server SHALL require [ITI-72] Incorporate Authorization Token in all [ITI-68] Retrieve Document requests, SHALL enforce the authorization decision in the token, and MAY further enforce policies beyond those made by the Authorization Server such as consent or business rules. 

scope: "ITI-68"

This scope request authorizes the full [ITI-68] transaction. This scope implicitly requests patient specific Read for Binary resources as defined in [ITI-68]. Further scope refinement is allowed in realm or project specific situations, these additional scopes would be in addition to the scope defined here. 



| **Editor: Please add rows to the following to ATNA Volume 1: section 9.2 ATNA Actor Options table**                      |
| add row after "STX WS-Security" for both Secure Node and Secure Application                                              |
|------------------------------------------------|
 
 "STX: HTTPS IUA" | ITI TF-1:9.2.6.7
 
 | **Editor: Please add section 9.2.6.7 as follows**      |
 |--------------------------------------------------------|
 
#### 9.2.6.7 STX: HTTPS IUA
The system will utilize server side authenticated TLS (also known as https) to authenticate the server to the client and provide communications integrity and encryption. The system will utilize the IUA Profile to authenticate the client application to the server (IUA Resource Server). See ITI TF-2a: 3.19.6.6.

| **Editor: Please add the following section to Volume 2 as follows**    |
|------------------------------------------------------------------------|

#### 3.19.6.6 STX: HTTPS IUA 

This configuration utilizes server side authenticated TLS (also known as https) to authenticate the server to the client and provide communications integrity and encryption; and the IUA Profile to authenticate the client application to the server (IUA Resource Server). 

The ATNA Local Secure Node shall be grouped with an IUA Authorization Client. The ATNA Remove Secure Node shall be grouped with an IUA Resource Server.
 
* TLS shall be server side authenticated, and may be client authenticated
* TLS shall be compliant with BCP195
* Local Secure Node shall reject connections that are not https, and may enforce other policies
* Remote Secure Node shall reject connections that do not carry a valid IUA token, and may enforce other policies



