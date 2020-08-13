**Integrating the Healthcare Enterprise**

![IHE\_LOGO\_for\_tf-docs](media/IHE-logo.jpeg)

**IHE ITI**

**Technical Framework Supplement**

**Internet User Authorization\
(IUA)**

**Trial Implementation**

Date: August 17, 2020

Author: ITI Technical Committee

Email: iti@ihe.net

**Please verify you have the most recent version of this document.** See [here](http://ihe.net/Technical_Frameworks/) for Trial Implementation and Final Text versions and [here](http://ihe.net/Public_Comment/) for Public Comment versions.

**Foreword**

This is a supplement to the IHE IT Infrastructure Technical Framework V11.0. Each supplement undergoes a process of public comment and trial implementation before being incorporated into the volumes of the Technical Frameworks.

This supplement is published on August 31, 2015 for trial implementation and may be available for testing at subsequent IHE Connectathons. The supplement may be amended based on the results of testing. Following successful testing it will be incorporated into the IT Infrastructure Technical Framework. Comments are invited and may be submitted at [http://www.ihe.net/ITI\_Public\_Comments](http://www.ihe.net/ITI_Public_Comments/).

This supplement describes changes to the existing technical framework documents.

"Boxed" instructions like the sample below indicate to the Volume Editor how to integrate the relevant section(s) into the relevant Technical Framework volume.

**Amend Section X.X by the following:**

Where the amendment adds text, make the added text **[bold underline]{.underline}**. Where the amendment removes text, make the removed text **~~bold strikethrough~~**. When entire new sections are added, introduce with editor's instructions to "add new text" or similar, which for readability are not bolded or underlined.

General information about IHE can be found at: [http://www.ihe.net](http://www.ihe.net/).

Information about the IHE IT Infrastructure domain can be found at: [http://www.ihe.net/IHE\_Domains](http://www.ihe.net/IHE_Domains/).

Information about the structure of IHE Technical Frameworks and Supplements can be found at: [http://www.ihe.net/IHE\_Process](http://www.ihe.net/IHE_Process/) and [http://www.ihe.net/Profiles](http://www.ihe.net/Profiles/).

The current version of the IHE Technical Framework can be found at: [http://www.ihe.net/Technical\_Frameworks](http://www.ihe.net/Technical_Frameworks/).

**CONTENTS**

[Introduction to this Supplement](#user-content-introduction-to-this-supplement)

[Problem Statement](#user-content-problem-statement)

[Background on the problem environment](#user-content-background-on-the-problem-environment)

[Open Issues and Question](#user-content-open-issues-and-question)

[Closed Issues](#user-content-closed-issues)

[General Introduction](#user-content-general-introduction)

[Volume 1 -- Profiles](#_Toc428776517)

[34 IUA Profile](#user-content-34-iua-profile)

[34.1 IUA Actors, Transactions, and Content Modules](#user-content-341-iua-actors-transactions-and-content-modules)

[34.1.1 Actor Descriptions and Actor Profile Requirements](#user-content-3411-actor-descriptions-and-actor-profile-requirements)

[34.1.1.1 Authorization Client](#user-content-34111-authorization-client)

[34.1.1.2 Authorization Server](#user-content-34112-authorization-server)

[34.1.1.3 Resource Server](#user-content-34113-resource-server)

[34.2 IUA Actor Options](#user-content-342-iua-actor-options)

[34.3 IUA Required Actor Groupings](#user-content-343-iua-required-actor-groupings)

[34.4 IUA Overview](#user-content-344-iua-overview)

[34.4.1 Concepts](#user-content-3441-concepts)

[34.4.1.2 Terminology](#user-content-3412-terminology)

[34.4.2 Use Cases](#user-content-3442-use-cases)

[34.4.2.1 Authorization](#user-content-34421-authorization)

[34.4.2.2 Delegation](#user-content-34422-delegation)

[34.5 IUA Security Considerations](#user-content-345-iua-security-considerations)

[34.6 IUA Cross Profile Considerations](#user-content-346-iua-cross-profile-considerations)


[Volume 2 -- Transactions 18](#user-content-volume-2----transactions)

[3.71 Get Authorization Token](#user-content-371-get-authorization-token)

[3.71.1 Scope](#user-content-3711-scope)

[3.71.2 Use Case Roles](#user-content-3712-use-case-roles)

[3.71.3 Referenced Standards](#user-content-3713-referenced-standards)

[3.71.4 Interaction Diagram](#user-content-3714-interaction-diagram)

[3.71.4.1 Get Authorization Token Request](#user-content-37141-get-authorization-token-request)

[3.71.4.1.1 Client Credential grant type](#user-content-371411-client-credential-grant-type)

[3.71.4.1.2 Authorization Code grant type](#user-content-371412-authorization-code-grant-type)

[3.71.5 Trigger Events](#user-content-3715-trigger-events)

[3.71.6 Message Semantics](#user-content-3716-message-semantics)

[3.71.6.1 JSON Web Token](#user-content-37161-json-web-token)

[3.71.6.2 SAML Token](#user-content-37162-saml-token)

[3.71.6.3 Authorization Grant Scope](#user-content-37163-authorization-grant-scope)

[3.71.7 Expected Actions](#user-content-3717-expected-actions)

[3.71.7.1 Client Credential grant type](#user-content-37171-client-credential-grant-type)

[3.71.7.2 Authorization Code grant type](#user-content-37172-authorization-code-grant-type)

[3.71.8 Message Examples](#user-content-3718-message-examples)

[3.71.9 Security Considerations](#user-content-3719-security-considerations)

[3.71.9.1 Security Audit Considerations](#user-content-37191-security-audit-considerations)


[3.72 Incorporate Authorization Token](#user-content-372-incorporate-authorization-token)

[3.72.1 Scope](#user-content-3721-scope)

[3.72.2 Use Case Roles](#user-content-3722-use-case-roles)

[3.72.3 Referenced Standards](#user-content-3723-referenced-standards)

[3.72.3.1 Related IHE Profiles](#user-content-37231-related-ihe-profiles)

[3.72.4 Interaction Diagram](#user-content-3724-interaction-diagram)

[3.72.5 Trigger Events](#user-content-3725-trigger-events)

[3.72.6 Message Semantics](#user-content-3726-message-semantics)

[3.72.6.1 JSON Web Token Option](#user-content-37261-json-web-token-option)

[3.72.6.2 SAML Token Option](#user-content-37262-saml-token-option)

[3.72.7 Expected Actions](#user-content-3727-expected-actions)

[3.72.8 Message Examples](#user-content-3728-message-examples)

[3.72.8.1 JSON Web Token Option](#user-content-37281-json-web-token-option)

[3.72.8.2 SAML Token Option](#user-content-37282-saml-token-option)

[3.72.9 Security Considerations](#user-content-3729-security-considerations)

[3.72.9.1 Security Audit Considerations](#user-content-37291-security-audit-considerations)


# Introduction to this Supplement

### Problem Statement

This profile is motivated by customer requirements for authorizing network transactions, when using HTTP RESTful transports. IHE has authorization profiles for the Web Services and SOAP based transactions. This profile provides an authorization profile for the HTTP RESTful transactions, e.g., browser based.

Being authorized means that the user, patient or provider, has legitimate access to this HTTP RESTful service. The authorization includes identifying the user, device, and or application that is making the request to the HTTP RESTful server, so that server can make further access control decisions.

The HTTP RESTful transport is being used by many healthcare applications and smart devices. These share a common set of issues. A typical use case example is:

-   The patient has a tablet and installs an application onto that tablet.

-   An application will need to retrieve and update health related data that is stored on a resource server. It uses HTTP RESTful transactions for both retrieve and update because HTTP support is integrated into the platform services.

-   The patient wants to configure the application to have access to their data without needing the IT staff at the application vendor and resource vendor to set things up.

The HTTP RESTful services may include user driven browser activity, downloaded applications, and automatic devices. The existing IHE ITI XUA Profile fills these needs for the SOAP transport based transactions. The existing IHE ITI EUA Profile fills these needs for various different transports within a single enterprise environment, including HTTP RESTful transports. The Basic Patient Privacy Consent (BPPC) Profile is associated with this profile and these other existing profile. BPPC covers the legal and administrative needs for consent documentation and associating the patient consent with policy documentation. This profile includes the ability to associate the electronic authorizations with the patient agreements and organizational policies.

Greater integration of this authorization with third party authorization and consent documentation profiles, such as those found in the IHE BPPC Profile, are a future effort. This profile starts with just the basic authorization activities.

It is important to understand that IUA is not a substitute for the administrative activities (such as withdrawing consent), policy setting, and other activities that BPPC documents.

The administrative actions needed to establish a third party as an authorization server for IUA is not covered by these actors or transactions. These activities are very much dependent upon the operational needs and privacy policies that apply to a particular deployment.

The IUA Profile does convey the identifiers and signatures needed to establish traceability between the Authorized HTTP RESTful transaction and the policies and consents behind that authorization.

### Background on the problem environment

One common pattern is to interact directly with the application to communicate with the authorization service. The application interacts with both patient and authorization service to support the granting of an access token. The application then saves the access token, and uses it to retrieve and update the health related data. Another common pattern is for the user to interact independently with the authorization service and obtain a token. This token is saved on the device for later use.

The key issues here are:

-   Reliable and accurate authorization decisions, as part of an overall privacy protecting and security environment.

-   Application developers want one common method for obtaining and using these tokens, not thousands. They want a method that is built into the common platforms, not one that must be added later, because it is difficult for end user oriented applications to modify the platforms.

-   Resource servers want one common method for receiving these tokens as part of HTTP RESTful transactions, and one common method for processing these tokens. (They will settle for a small number of methods if they must.)

-   Users, patients and providers, want to be in control, do not want to depend on support staff to set up their devices and applications, and want to minimize the interference from authorization requirements.

Similar issues arise with:

-   In house application distribution that needs authorization for devices used within the facility.

-   The in house IT staff wants a common method to authorize use of in house web applications and access to in house resources.

-   IT staff are more willing to run their own internal authentication and authorization servers, but want to use off the shelf software and want the option to outsource these services. They are more likely to separate authentication from authorization than end user systems. Authentication issues are closely related to HR activities like hiring and firing. Authorization issues are related to patient and work assignments. These are controlled by different parts of the organization and have different process dependencies.

-   Providers and Specialists have authorization needs for dealing with other organizations, need to deal with many resource services an may struggle to maintain the amount of different authentication and authorization relationships.

-   Granting subset access to specialized provider. E.g., read access to cardiac info to physical therapy organization, forbidding access to other sensitive health data.

There are also environmental assumptions made by this profile.

First, it is assumed that there will many systems working together to build the access control environment, where IUA provides one part only. For example, a glucose monitor may be authorized to have access to a patient's medical record. The expectation is that this will mean access to all of the glucose related information, which will include a variety of measurements and prescriptions. But, it is expected that if the device requests other sensitive health data about it will be rejected.

Second, this profile is operating in an environment where access consents are managed by BPPC or other mechanisms. IUA is not a substitute for documenting, establishing, and modifying these legal agreements. For example, there will be a documented consent agreement between a patient and a provider that the provider will provide medical records to a healthcare proxy that is identified and authorized by the patient. BPPC is one way to document that agreement.

# Open Issues and Question

- **Issue 1**: This profile does not specify the internal structure of "client_id". This is a major concern for operations and security management. But, OAuth does not provide a full specification for client_id. It just specifies its purpose.
DICOM's equivalent information attributes are: Manufacturer, Model, Software Versions, and Serial Number.
The OAuth client ID must identify the device, the application (including any necessary version information), the particular instance, and any other information needed to identify the client application uniquely. Registration of clients is a significant operational and security problem that is being postponed until there is more experience with problems in the field and reasonable solutions. There is known danger from spoofing of client_id. At this time, the method for assignment of client_id is not included in the profile. In the field there are a variety of methods being tried. Many depend upon physical distribution methods or out of band communications to manage the authentication problems.

- **Issue 2**: This profile mandates support for JWT token format. It has an XUA SAML Option defined by IHE for ease of integration with the IHE WS-Security environment. You may also use other token formats as part of a deployment.

- **Issue 3**: Audit messages are only defined for clients that are also Secure Applications. There is no defined auditing for other clients.

# Closed Issues

- **Issue 4**: This profile does not require client grouping with Secure Node or Secure Application because it is using the OAuth issuance rules for client_id. It assumes that the client_id management will deal with these security considerations in a manner similar to the certificate management assumptions made for TLS and other certificate users.

- **Issue 8**: This profile uses the Authorization header only for conveying the authorization information. The parameter form is not prohibited but is not compliant with the profile.

- **Issue 9**: This profile does not explain the ways that some Resource Servers utilize HTTP redirects to automate some kinds of authorization activities. The actual HTTP transactions used for Obtain Authorization Token and Authorized RESTful Transaction are as defined within this profile. The other transactions are under the control of the Resource Server and its design.

- **Issue 10**: The selected standards are: The OAuth 2.0 Framework, JWT Token, with defined extensions, SAML Token, using the XUA extensions.                 |


# General Introduction

Update the following Appendices to the General Introduction as indicated below. Note that these are not appendices to Volume but rather to the General Introduction.

**Appendix A - Actor Summary Definitions**

Add the following actors to the IHE Technical Frameworks General Introduction list of actors:

|Actor                |Definition
|-----                |----------
|Authorization Client |A client that presents access tokens as part of transactions.
|Authorization Server |A server that provides access tokens to requesting clients.
|Resource Server      |A server that provides services that need authorization.


**Appendix B - Transaction Summary Definitions**

Add the following transactions to the IHE Technical Frameworks General Introduction list of Transactions:

|Transaction                                |Definition
|-----------                                |----------
|Incorporate Authorization Token \[ITI-72\] |Add an access token to a transaction.
|Get Authorization Token \[ITI-71\]         |A transaction that is used to request and obtain an access token for use in Authorized transactions.


# Volume 1 -- Profiles

# 34 IUA Profile

The IUA Profile adds authorization information to HTTP RESTful transactions. The IUA actors and behavior will be added to other profiles and transactions that need authorization.

## 34.1 IUA Actors, Transactions, and Content Modules

The actors in the IUA Profile manage the tokens used for authorization of access to HTTP RESTful services. The Authorization Client provides the access token that is incorporated into HTTP RESTful transactions to indicate that this transaction is authorized. The Authorization Client can also manage the interactions with an Authorization Server to obtain the access token.

The OAuth 2.1 Authorization Framework requires client identification, which may be based on a *client_id* parameter [OAuth 2.1, Section 2.2]. Depending on the grant type, the use of the *client_id* MAY be required. For example the *Authorization Code* grant type requires the use of the *client_id* for client identification [OAuth 2.1, Section 4.1], while the *Client Credential* grant type does not [OAuth 2.1, Section 4.2].

The OAuth 2.1 Authorization Framework also requires client authentication for confidential and credential clients [OAuth 2.1, Section 2.3]. It recommends the use of to use asymmetric (public-key based) methods for client authentication [OAuth 2.1, Section 9.1], but allows other suitable HTTP based authentication schemes matching the security policy of the Authorization Server [OAuth 2.1, Section 2.3.2].

This profile requires the use of a *client_id* for client identification and a *client_secret* used with the HTTP Basic Authentocation scheme for client authentication of confidential and credential clients, if no other methods for identification and authentication are used.  
Depending on the grant type, the OAuth 2.1 Framework also requires user authentication. For example, the *Authorization Code* grant type covered by this profile requires user authentication [OAuth 2.1, Section 4.1], while the *Client Credential* grant type does not [OAuth 2.1, Section 4.2]. The methods used by the authorization server to authenticate the user (e.g., username and password login, session cookies, delegation to Authentication Server) is not scoped in the OAuth 2.1 Authorization Framework [OAuth 2.1, Section 3.1].

Since user authentication methods chosen depend on the projects or national security policy, they are not scoped in this profile and SHALL be defined in the specific implementation projects or national extensions of this profile. If the user authentication is not implemented in the Authorization Server, the use of OpenID Connect with the Authorization Grant or Hybrid flow is recommended.

It is the responsibility of the Resource Server to enforce the access policies based on the transaction performed and the information provided in the access token. Therefore the Resource Server must be able to rely upon the decisions made by the Authorization Server (e.g., client identification, user authentication), which requires that a trust relation between the Resource Server and the Authorization Server was established beforehand.  

The Ressource Server may delegate the access policy enforcement to actors it is grouped with by providing the information from the access token and transaction data, or to other actors (e.g., by implementing the Authorization Decisons Verifier actor of the Secure Retrieve (SeR) supplement).

Note: An analogy of the segregation of duties for access control between the Authorization Server and the Resource Server is given in a  textbook (*Solving Identity Management in Modern Applications*, *APress 2019* by Yvonne Wilson and Abhishek Hingnikar) comparing the authorization and policy enforcement with a ticketing and entrance control to events (e.g, opera, cinema). In this analogy the Authorization Server provides the ticket which authorizes participation, while additional checks are performed to finally particpate to the event.  

This profile relies on the OAuth 2.1 Authorization Framework. Since the original publication of OAuth 2.0 in 2012, several new RFCs have been published that add or remove functionality from the core specification. Version 2.1 of the OAuth Authorization Framework consolidates and simplifies the most commonly used features and best practices of OAuth 2.0.

![IUA Actor Diagram](media/1.1_IUA-actor-diagram.png)

Figure 34.1-1: IUA Actor Diagram

Table 34.1-1 lists the transactions for each actor directly involved in the IUA Profile. To claim compliance with this profile, an actor shall support all required transactions (labeled "R") and may support the optional transactions (labeled "O").

Table 34.1-1: IUA Profile - Actors and Transactions

|Actors               |Transactions                     |Optionality	|Reference      
|----                 |----                             |---        	|-----          
|Authorization Client |Incorporate Authorization Token  |R          	|ITI TF-2c: 3.72
|                     |Get Authorization Token          |O          	|ITI TF-2c: 3.71
|Authorization Server |Get Authorization Token          |R          	|ITI TF-2c: 3.71
|Resource Server      |Incorporate Authorization Token  |R          	|ITI TF-2c: 3.72

### 34.1.1 Actor Descriptions and Actor Profile Requirements

The IUA actors are expected to be combined with other actors that perform HTTP RESTful transactions. Combining an Authorization Client with another actor means that this other actor will provide an access token as part of the HTTP transaction to a HTTP RESTful server. It may perform the Get Authorization [ITI-71] transaction to obtain the access token. The corresponding HTTP RESTful server should be combined with the Resource Service to indicate that the server can perform access control.

#### 34.1.1.1 Authorization Client

The Authorization Client performs the network transactions and user interactions needed to obtain an access token and to attach that token to transactions to indicate that those transactions are authorized. An Authorization Client in IUA supports the following associated transactions:

-   Incorporate Authorization Token: In this case the access token has already been obtained and is communicated as part of the HTTP RESTful transaction for some other profile or service. This token indicates that the HTTP RESTful transaction has been authorized by the Authorization Server by an authenticated person.

-   Get Authorization Token: In this use, the Authorization Client actor interacts with an Authorization Server to obtain a token that indicates HTTP RESTful transactions for a particular kind of service and device are authorized by the user. This may include interactions with the user for authentication purposes.

#### 34.1.1.2 Authorization Server

The Authorization Server provides access tokens to requesting clients. In IUA, the Authorization Server uses an authenticated user identity, the requested HTTP RESTful service URL, and other information to determine whether HTTP RESTful transactions are authorized. If authorized, the Authorization Server provides a token indicating that HTTP RESTful service access is authorized.

#### 34.1.1.3 Resource Server

The Resource Server provides services to access protected resources that need authorization. In IUA the Resource Server accepts a HTTP RESTful transaction request with an incorporated access token. It evaluates the access token to verify that the Authorization Server has authorized the transaction. The Resource Server must enforce this authorization and may perform additional authorization decisions that are specific to the requested service. The Resource Server may then allow the transaction to proceed, subject to access control constraints that may also be in place.

Notes:

1. The Resource Server and Authorization Server actors MAY be grouped into an integrated product together with user authentication, access control, and other services.

2. Many Resource Servers will perform additional access control decisions and may restrict responses even for authorized transactions.

3. Resource Server MAY declare support for IUA in their CapabilityStatement using the element **CapabilityStatement.rest.security.**


## 34.2 IUA Actor Options

The **SAML Token Option** enables integration of environments that use both, SAML access token and the OAuth authorization infrastructure. All actors SHALL support the JSON Web Token option and may support the SAML Token option.


Table 34.2-1: IUA - Actors and Options

| IUA Actor            | Option             |Optionality
|----------------------|--------------------|----------	
| Authorization Client | JWT Token          |R    		
|                      | SAML Token         |O    		
| Authorization Server | JWT Token         	|R    		
|                      | SAML Token			|O          
| Resource Server      | JWT Token 			|R    		
|                      | SAML Token         |O    		        


## 34.3 IUA Required Actor Groupings

An actor from this profile shall implement the required transactions and/or content modules in this profile ***in addition to*** all of the transactions required for the grouped actor (Column 2).


  |IUA Actor            |Actor to be grouped with   |Reference                    |Content Bindings Reference
  |----                 |-----                      |-----                        |-----                      
  |Authorization Server |Time Client                |ITI TF-1:7 Consistent Time   |                           
  |Resource Server      |Time Client                |ITI TF-1:7 Consistent Time   |                           
  |Authorization Client |                           |                             |                           


## 34.4 IUA Overview

### 34.4.1 Concepts

The term "authorization" and "access control" are used colloquially for a variety of related activities. All of the concepts listed below are sometimes called "authorization" or "access control". See the IHE ITI Access Control whitepaper for a detailed discussion of Access Control concepts. This profile will use more specific terms for each of these activities. These are:

-   Provisioning -- Setting up the initial rules and updating them when the situation changes. The administrator may say "Authorize Dr. X to have access". The steps taken to make this happen are called provisioning.

-   Delegation -- Adding, transferring and revoking authorization from one person to another. This is closely related to provisioning. It differs in that it can only transfer authority that has already been provisioned, and it may track changes to provisioned access for the original person.

-   Authentication -- Determining that the actual user (at the moment of authentication) is the claimed identity.

-   Authorization -- Determining that the authenticated user is authorized to have access to a resource (at the moment of authorization). The profile describes how to convey an access authorization decision. It is not defining how the decision is made.

-   Access Control -- A system of provisioning, delegation, authentication, and authorization. It is normal to have multiple nested levels of access control. This profile is concerned with whether access is allowed to make the HTTP transaction requests to the specified resources. There are likely also building access controls, resource server access controls, and other access controls involved.

### 34.4.1.2 Terminology

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in "Key words for use in RFCs to Indicate Requirement Levels" [RFC 2119]. The interpretation should only be applied when the terms appear in all capital letters.

This profile uses the terms "access token", "refresh token", "authorization server", "resource server", "authorization endpoint", "authorization request", "authorization response", "token endpoint", "grant type", "access token request", and "access token response" as defined by The OAuth 2.1 Authorization Framework [OAuth 2.1]. 

In accordance with the definitions in the OAuth 2.1 Authorization Framework [OAuth 2.1] this profile distinguishes confidential clients and public clients as follows:

- *confidential client* - a client which stores the client authentication data (e.g., client\_id and client\_secret) in a way, that the user has no access to it (e.g., a server hosted web application).

- *credentialed client* - a clients which has credentials, but their identity has been not been confirmed by the Authorization Server.

- *public client* - a client where the user (in principle) has access to the client code and client data in principle. Public clients cannot store client authentication data in a confidential way (e.g., single page web applications, native mobile apps on a device, if no additional features are implemented to make the client authentication data unavailable for the user).

Note:

- A public client classification does not automatically mean the client is unsecure. Public clients typically are under the full control of the user (e.g., a native app on the users device) and secured againts malicious attacks. Public clients just cannot hide authentication data from the user rendering client authentication useless.   

The OAuth 2.1 Authorization Framework uses the term "resource owner" for the user an authorized client may access data on behalf of. Typically in health related environments a healthcare professional access patients or organization related data (resoures) for which the healthcare professional is not the "legal owner" but may access according to the access policies of the environment. To avoid any misunderstandings related to the OAuth term "resource owner" a the "legal owner", this profile uses the term "user" instead.


### 34.4.2 Use Cases

#### 34.4.2.1 Authorization

This profile applies to use cases where a user authorizes an client application to access health data behalf of the user using OAuth. Beyond other, relevant use cases are:   

A healthcare professional uses a server hosted web application to access a patients electronic health record (EHR) using RESTful transactions. The web application has been registered beforehand at the Authorization Server with client ID and client authentication method (e.g. client secret) by a system administrator. When accessing a view on the EHR, the browser is redirected to the EHR Authorization Server. The Authorization Server authenticates the healthcare professional either by presenting the views to enter the authentication factors (e.g. username, password and 2nd factor) or by redirecting to an Identity Provider (IdP). This step may be omitted, if the browser already has an authenticated session (e.g. session cookie). After user authentication, the Authorization Server performs the necessary steps to authorize the web application access to the EHR data, either by contract or by explicit consent given by the healthcare professional. When authorized, the web application retrieves an access token which authorizes it to request and retrieve the EHR data from the Resource Server(s) on behalf of the healthcare professional.

A healthcare professional uses a single page web application to access a patients electronic health record (EHR) using RESTful transactions. At initial startup the app registers with the Authorization Server using a dynamic client registration protocol. When accessing a view on the EHR, the steps follow the same steps as in the web application use case above.   

A clinical monitor managed by the hospital system administrators access a patients EHR using RESTful transactions in the hospital LAN. At installation time, clinical monitor has been registered at the Authorization Server with client ID and client authentication method (e.g. client secret) by the system administrator and a contracts (policies) have been deposited at the Authorization Server and Resource Server(s) authoriziing access to the EHR. Before accessing patient EHR data, the clinical monitor requests an access token freom the Authorization Server using the client credential grant type. The clinical monitor incorperates the access token to the RESTful transactions to access EHR data and documents stored in the EHR Resource Server(s).         

A patient uses a native app on her mobile device to access data from her electronic health record (EHR) using RESTful transactions via the internet. At first startup the app registers with the Authorization Server using a dynamic client registration protocol. When accessing a view on the EHR, the native app is redirected to the EHR Authorization Server, which authenticates the patient either by presenting the views to enter the authentication factors (e.g. username, password and 2nd factor) or by delegating to an Identity Provider (IdP). After user authentication, the Authorization Server performs the necessary steps to authorize the native app to access to the EHR data by explicit user consent. When authorized, the native app retrieves an access token which authorizes the app to request and retrieve the EHR data from the Resource Server(s) on behalf of the patient.

#### 34.4.2.2 Delegation

There are multiple reasons to perform delegations. These cases primarily involve patient delegation choices. Providers rarely have the authority to delegate. IT staff may use delegation as part of the support for autonomous devices.

Users may delegate authority to:

-   Device or applications that are performing a service for the patient, for example automatic glucose monitors that can provide monitoring records and receive control information from a healthcare provider service that is providing diabetic care.

-   Advocates and proxies who are authorized by the patient to make decisions for the patient.

-   Organizations that are acting for the patient, such as a visiting nurse organization that is providing support to the patient.

Revocation of delegation needs to be clearly specified by policy. Revocation may be removal of rights because of swapping devices. Expiration, re-authorization, etc. also need to be covered. Revocation is not just a response to breaches and failures. Revocation is a normal response to changes in people, equipment, and relationships.

# 34.5 IUA Security Considerations

IUA uses OAuth 2.1 which contains references to security analyses. There are also a variety of analyses available in the public literature. This profile does not introduce new considerations to those analyses. We have not identified any new healthcare related issues.

For confidential clients this profiles requires client authentication using client\_id and client\_secret, if no other reliable client authentication method is used, and the client registration with a fixed redirect\_uri.

IUA does not address issues around issuing and revoking client\_ids. OAuth 2.1 relies upon the client\_id for client identification and authorization. OAuth 2.1 does not further define how client\_ids are managed.

Usually Authorization Server publish web forms where system administrators and users can apply for a client_ID. OAuth 2.1 defines a mechanism for dynamically registering clients with authorization servers, by defining a set of desired client metadata values to be made available to the authorization servers [OAuth 2.1, Section 2].  

The Authorization Server will have an administratively managed list of approved client\_ids for accepted clients. This list will be updated as new clients are approved or existing clients are removed. An access token will not be issued for unapproved clients. This assumes that the client\_id management will deal with these security considerations in a manner similar to the certificate management assumptions made for secure communication transactions.

# 34.6 IUA Cross Profile Considerations

The XUA profile provides equivalent functionality for SOAP based transactions. Both profiles, XUA and IUA define a transaction to incorporate a token to transactions accessing protected data. Both profiles have much in common, but also some remarkable differences:

- The XUA profile defines a transactions to retrieve an SAML 2 assertion for authorization (Get X-User Assertion), but does not specify it in detail, leaving the details to national extensions and project specific implementations. In contrast the IUA profiles specifies the analog Get Authorization Token [ITI-71] for OAuth 2.1 compliant access token.

- While the XUA profile relies on ATNA Node Authentication to authenticate the client (or client network node), IUA uses the mechanism defined in the OAuth 2.1 Authorization Framework to authenticiate client applications.

- While XUA supports SAML 2 Assertions only, the IUA profile supports access token in JWT and SAML 2.0 Assertion format.  

The SAML token option in IUA enables an Authorization Client actor to incorporate access token originally retrieved and issued from a XUA X-Assertion Provider and use it in the Incorporate Authorization Token [ITI-72] transaction, when accessing protected data from a Resource Server via RESTful transactions.   

# Volume 2 -- Transactions

**Add Section 3.71**

# 3.71 Get Authorization Token

This transaction is used by Authorization Client actors to obtain an OAuth 2.1 compliant access token for use in a RESTful transaction to access data from a Resource Server actor.

The OAuth 2.1 Authorization Framework [OAuth 2.1, Section 4] defines the following authorization grant types:

-   *Authorization Code Grant* [OAuth 2.1, Section 4.1]. This grant type is optimized for confidential clients who make use of User Agents (e.g., web browsers).

-   *Client Credentials Grant* [OAuth 2.1, Section 4.2]. This grant type is optimized for clients requesting access tokens using only its client credentials and is restricted to confidential clients (e.g., medical devices, backend applications).

The OAuth 2.1 Authorization Framework further defines extension points to implement extension grant types [OAuth 2.1, Section 4.3], e.g.:

- *Device Authorization* \[RFC 8628]. This grant type is optimized for devices that cannot use a browser to perform a user-agent- based authorization or don’t provide interfaces for the user to input text required for authorization and authentication (e.g., medical devices, mobile health sensors).

This profile is scoped to the *Authorization Code* and *Client Credential* grant types. To claim compliance with this profile, the Authorization Server actor SHALL support the *Authorization Code* and *Client Credential* grant type and MAY support the *Device Authorization* or other OAuth 2.1 extension grant types.   

### 3.71.1 Scope

This transaction SHALL be used by Authorization Client actors to retrieve an OAuth 2.1 compliant access token defined in Section 3.71.6 Message Semantics of this profile.

### 3.71.2 Use Case Roles

This profile defines the following actors and roles:

Table 3.71.2-1: Actor Roles

|Actor                  |Role                                                           |
|-------                |-----                                                          |
|Authorization Client   | Authorization portion of a HTTP RESTful transaction client    |
|Authorization Server   | Server that grants access tokens.                             |


### 3.71.3 Referenced Standards

This transaction relies on standards defined in the following documents and the references therein: 

- *OAuth 2.1*: The OAuth 2.1 Authorization Framework, published as draft-ietf-oauth-v2-1-00, July 30, 2020.

- *JWT Access Token*: JSON Web Token (JWT) Profile for OAuth 2.0 Access Tokens, published as draft-ietf-oauth-access-token-jwt-07, April 2020.

- *RFC 7519*: JSON Web Token (JWT), May 2015.  

- *RFC 7522*: Security Assertion Markup Language (SAML) 2.0 Profile for OAuth 2.0 Client Authentication and Authorization Grants, May 2015. 

- *RFC 7515*: JSON Web Signature (JWS), May 2015. 

- *RFC 7518*: JSON Web Algorithms (JWA), May 2015. 

- *HEART scopes*: Health Relationship Trust Profile for Fast Healthcare Interoperability Resources (FHIR) OAuth 2.0 Scopes, July 2018. 


### 3.71.4 Interaction Diagram

![ITI-71 Flow Diagram](media/basic-flow.png)

Figure 3.71.4-1: Basic Process of the Authorization Token Request and Incorporate Authorization Token transaction

```
\@startuml

group Get Authorization Token \[ITI-71\]
AuthorizationClient -> AuthorizationServer : Authorization Request
AuthorizationClient <- AuthorizationServer : Authorization Response + Authorization Token
end

group Incorporate Authorization Token \[ITI-72\]
AuthorizationClient -> ResourceServer : Resource Request + Authorization Token
AuthorizationClient <- ResourceServer : Resource Response
end

\@enduml
```

Main Flow:

1.  The Authorization Client authenticates to the Authorization Sever and provides claims related to the intended request to acces protected resources of the Resource Server.

2.  The Authorization Server authenticates the client, validates the claims against the user consent and generates an access token that authorizes the Authorization Client actor to request the protected resources from the Resource Server.

3. The Authorization Server incorporates the access token to the requests of the protected resources to the Resource Server. 

4. The Resource Server evaluates the access token and the resource request and enforces the access policies. 


#### 3.71.4.1 Get Authorization Token Request

The sequence of HTTP(S) requests to perform an Get Authorization Token transaction depends on the grant type chosen.

##### 3.71.4.1.1 Client Credential grant type

![ITI-71 Client Credential](media/client-credential-grant.png)

Figure 3.71.4.1.1-1: Sequence of HTTP requests in the client credential grant type.


The Authorization Client actor requests an access token using client credentials (or other supported means of authentication). This grant type SHALL be used by confidential clients only [OAuth 2.1, Section 4.2].

The Authorization Client actor makes a HTTP(s) POST request to the token endpoint with the following parameters in the HTTP request entity-body [OAuth 2.1, Section 4.2.2]:

- *grant_type* (REQUIRED): The value of the parameter SHALL be *client_credentials*.

- *resource* (REQUIRED): Single valued identifier of the Resource Server api endpoint to be accessed [JWT Access Token, Section 3].

- *scope* (OPTIONAL): The scope claimed by the Authorization Client.

The request SHALL use the *application/x-www-form-urlencoded* format with a character encoding of UTF-8 [OAuth 2.1, Section 4.4.2].

A non-normative example of the access token request with client authentication using the *client_id* and *client_secret* in the HTTP Authorization header, MAY be as follows: 

```
POST /token HTTP/1.1
Host: server.example.com
Authorization: Basic czZCaGRSa3F0MzpnWDFmQmF0M2JW
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials
&scope=scope_1 scope_2 ... scope_N
&resource=https://rs.example.com/
```

If the access token request is valid and authorized, the Authorization Server responds the access token response message in JSON format with the following attributes [OAuth 2.1, Section 4.2.3]:

- *token_type* (REQUIRED): The value of the parameter SHALL be *Bearer*.

- *access_token* (REQUIRED): The access token as JSON Web Token or SAML 2.0 assertion as described below.

- *scope* (REQUIRED): The scope granted by the Authorization Server.

- *expires_in* (OPTIONAL): This parameter MAY be used to inform the Authorization Client how long the access token is valid.  

The access token response MAY contain other parameter or extensions depending on the implementation details of the Authorization Server actor [OAuth 2.1, Section 4.2.3].

The Authorization Server SHALL include the HTTP *Cache-Control* response header field with value *no-store* and the *Pragma* response header field value *no-cache* to the access token response [OAuth 2.1, Section 4.2.3].

A non-normative example of the access token response is as follows:

```
HTTP/1.1 200 OK
Content-Type: application/json
Cache-Control: no-store
Pragma: no-cache
{
  "token_type": "Bearer",
  "access_token": "2YotnFZFEjr1zCsicMWpAA",
  "scope": scope_1 scope_2 ... scope_M
  "expires_in": 3600,
  "example_parameter": "example_value"
}
```

The Authorization Server SHALL respond an error response as defined in the OAuth 2.1 Authorization Franework [OAuth 2.1, Section 5.2] if the request does not match the requirements or is not understood.  


##### 3.71.4.1.2 Authorization Code grant type

![ITI-71 Authorization Code](media/authorization-code-grant.png)

Figure 3.71.4.1.1-1: Sequence of HTTP requests in the client authorization code and PCKE grant type.

This grant type SHALL be used by confidential, credential and public clients, if the explicit consent of the user is required to authorize the Authorization Client to access data on behalf of the user.

The Authorization Client actor directs the user-agent to make a HTTP GET request to the authorization endpoint with the following parameters using the "application/x-www-form-urlencoded" format [OAuth 2.1, Section 4.1.1.3]:

- *response_type* (REQUIRED): The value must be *code*.

- *client_id* (REQUIRED, IF KNOWN): The identifier the Authorization Client is registered at the Authorization Server.

- *state* (REQUIRED): An unguessable value used by the client to track the state between the authorization request and the callback to the redirect URI. While this parameter is optional in the OAuth 2.1 Authorization Framework [OAuth 2.1, Section 4.1.1.3] it is required in this profile for security reasons. 

- *resource* (REQUIRED): Single valued identifier of the Resource Server api endpoint to be accessed [JWT Access Token, Section 3].

- *code_challenge* (REQUIRED): A challenge derived from the client generated code verifier used to correlate the authorization request to the token request [OAuth 2.1, Section 4.1.1 and references therein]. 

- *code_challenge_method* (OPTIONAL): Indicator used for the code challenge transformation method. It's value MAY be *plain* or *S256* [OAuth 2.1, Section 9.8].  

- *redirect_uri* (OPTIONAL): The absolute URI of the Authorization Client callback endpoint to which the authorization server will send the user agent back once access is granted (or denied). This parameter is required if the Authorization Client is registered at the Authorization Server with multiple redirect URI, optional otherwise [OAuth 2.1, Section 3.1.2.3].  

- *scope* (OPTIONAL): The scope claimed by the Authorization Client.

A non-normative example of the authorization request is as follows:

```
GET /authorize?response_type=code&
client_id=s6BhdRkqt3&
state=xyz&
redirect_uri=https%3A%2F%2Fclient%2Eexample%2Ecom%2Fcb&
code_challenge=6fdkQaPm51l13DSukcAH3Mdx7_ntecHYd1vi3n0hMZY&
code_challenge_method=S256&
resource=https%3A%2F%2Frs.example.com%2F
&scope=scope_1%20scope_2%20scope_N 
HTTP/1.1
Host: server.example.com
```

If the user grants the access request, the Authorization Server directs the user agent to the Authorization Clients redirect URI with the authorization response parameter in the *application/x-www-form-urlencoded* format. The response parameter SHALL be as follows:

- *code* (REQUIRED): The authorization code generated by the Authorization Server.  

- *state* (REQUIRED): An unguessable value used by the client to track the state between the authorization request and the callback.

```
HTTP/1.1 302 Found
Location: https://client.example.com/cb?code=SplxlOBeZQQYbYS6WxSbIA&state=xyz
```

The Authorization Client SHALL use the *authorization code* in an access token request to retrieve an access token and token metadata from the Authorization Server. It makes a HTTP POST request to the token endpoint with the following parameters in the HTTP request entity-body [OAuth 2.1, Section 4.1.3]:   

- *grant_type* (REQUIRED): The value SHALL be "authorization_code".

- *code* (REQUIRED): The authorization code received from the Authorization Server in the authorization response.

- *redirect_uri* (REQUIRED): The redirect URI of the Authorization Client callback. The value SHALL match the redirect URI the Authorization Client is registered at the Authorization Server and the value of the *redirect_uri*, if presented in the authorization request. 

- *client_id* (REQUIRED): The client ID the Authorization Client is registered with at the Authorization Server, if no othe authentication scheme is used for client authentication.

- *code_verifier*: The original code verifier string. REQUIRED, if the "code_challenge" parameter was used in the authorization request. SHALL NOT be used otherwise. 


A non-normative example of the access token request with client authentication using the *client_id* and *client_secret* in the HTTP Authorization header, MAY be as follows:

```
POST /token HTTP/1.1
Host: server.example.com
Authorization: Basic czZCaGRSa3F0MzpnWDFmQmF0M2JW
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code
&code=SplxlOBeZQQYbYS6WxSbIA 
&redirect_uri=https%3A%2F%2Fclient%2Eexample%2Ecom%2Fcb
&code_verifier=3641a2d12d66101249cdf7a79c000c1f8c05d2aafcf14bf146497bed
```

If the access token request is valid and authorized, the Authorization Server responds with an access token response message in JSON format with the following attributes [OAuth 2.1, Section 4.1.4]:

- *token_type* (REQUIRED): The value of the parameter SHALL be *Bearer*.

- *access_token* (REQUIRED): The access token as JSON Web Token or SAML 2.0 assertion as described below.

- *scope* (REQUIRED): Used to inform the client which scopes were granted by the Authorization Server [OAuth 2.1, Section 3.3]. 

- *expires_in* (OPTIONAL): This parameter MAY be used to inform the Authorization Client on the access token lifetime.

- *refresh_token* (OPTIONAL): A token provided by the Authorization Server which can be used by the Authorization Client to obtain new access tokens using the same authorization grant.  

The access token response MAY contain other parameter or extensions depending on the implementation details of the Authorization Server actor[OAuth 2.1, Section 4.2.3].

The Authorization Server SHALL include the HTTP *Cache-Control* response header field with value *no-store* and the *Pragma* response header field value *no-cache* to the access token response.

A non-normative example of the access token response is as follows:

```
HTTP/1.1 200 OK
Content-Type: application/json
Cache-Control: no-store
Pragma: no-cache

{
"token_type": "Bearer",
"access_token": "2YotnFZFEjr1zCsicMWpAA",
"scope": scope_1 scope_2 ... scope_M
"expires_in": 3600,
"refresh_token": "tGzv3JOkF0XG5Qx2TlKWIA",
"example_parameter": "example_value"
}
```

The Authorization Server SHALL respond an error response as defined in the OAuth 2.1 Authorization Franework [OAuth 2.1, Section 5.2 and 4.1.2.1] if a request does not match the requirements or is not understood. 


### 3.71.5 Trigger Events

This transaction takes place whenever an Authorization Client needs an access token authorizing a HTTP RESTful transaction. This may be due to expiration of an existing token, a resource request has indicated that a new token is required, configuration or installation of a device, or as a routine request for new transactions.


### 3.71.6 Message Semantics

#### 3.71.6.1 JSON Web Token

In the JSON Web Token option the access token is defined as JSON object with the follwing attributes: 

- *iss* (REQUIRED): A single valued string identifying the instance which issued the access token (e.g.,the Authorization Server) [JWT Access Token, Section 2.2]. 

- *sub* (REQUIRED): If known, unique identifier of the user; the *client_id* otherwise [JWT Access Token, Section 2.2].  

- *aud* (REQUIRED): Single valued identifier of the Resource Server api endpoint to be accessed [JWT Access Token, Section 2.2]. This parameter SHALL match the *resource* parameter claimed by the Authorization Client. 

- *jti* (REQUIRED): A unique identifier for the JWT access token [JWT Access Token, Section 2.2]. 

- *exp* (REQUIRED): Expiration time of the token in Numeric Date format [JWT, Section 4.1.4]. 

- *scope* (REQUIRED): The scope granted by the Authorization Server [JWT Access Token, Section 2.2.3].   

- *nbf* (OPTIONAL): The earliest time in Numeric Date format the token SHALL be accepted [JWT, Section 4.1.5].  

- *iat* (OPTIONAL): The issuing date in Numeric Date format [JWT, Section 4.1.6]. 


The JWT access token MAY contain other parameter or extensions depending on the implementation details.

The Authorization Client, Authorization Server, and Resource Server SHALL support the optional extensions defined in table 3.71.6.1-1. If present, the claims shall be wrapped in an "extensions" claim object that consists of the key 'ihe\_iua' and a value of a JSON object containing the claims, as such

```
"extensions" : {  
  "ihe_iua" : {  
    "subject_id":"John Iyouay",  
    ...  
  }  
}
```

The claim content shall correspond to the content defined in the XUA specification (see ITI TF-2b: 3.40.4.1.2 Message Semantics). The encoding of the Subject Role and Purpose of Use MUST be as JSON arrays.

Table 3.71.6.1-1: JWT Claims of the IUA extension

|JWT Claim                      |Optionality|Definition                                       	
|-------------------------------|---------	|----------------
|subject\_name                  |O	 		|Plain text user's name
|subject\_organization          |O    		|Plain text description of the organization
|subject\_organization\_id      |O   		|Unique identifier of the organization 
|subject\_role                  |O	 		|Coded value indicating the user's role 
|purpose\_of\_use               |O	 		|Purpose of use for the request   
|home\_community\_id            |O	 		|Home community ID where the request originated
|national\_provider\_identifier |O    		|
|person\_id                     |O	 		|Patient ID, Citizen ID, or other similar public ID used for health identification purposes


TBD: put all BPPC related attributes in a BPPC extension. 


Table 3.71.6.1-2: JWT Claims of the BPPC extension

|JWT Claim                      |Optionality|Definition                                       	
|-------------------------------|---------	|----------------
|patient\_id                    |O	 		|Patient ID related to the Patient Privacy Policy Identifier
|doc\_id                        |O	 		|Patient Privacy Policy Acknowledgement Document ID
|acp                            |O	 		|Patient Privacy Policy Identifier


The mapping of parameter of the JWT access token to a XUA compliant SAML 2.0 Assertion is shown in table Table 3.71.6.1-3 below.  

Table 3.71.6.1-3: JWT Claims and corresponding XUA Assertion attributes

|JWT Claim                      |XUA Attribute              
|-------------------------------|---------------------------
|subject\_name                  |SubjectID
|subject\_organization          |SubjectOrganization
|subject\_organization\_id      |SubjectOrganizationID
|home\_community\_id            |HomeCommunityID 
|national\_provider\_identifier |NationalProviderIdentifier
|subject\_role                  |Subject:Role 
|doc\_id                        |docid
|acp                            |acp
|purpose\_of\_use               |PurposeOfUse
|patient\_id                    |Resource-ID


The Authorization Client and Authorization Server actors SHALL support signed JWT token as specified in JSON Web Signature [RFC 7515]. Any actor that supports this transaction MAY support the JWE (unsigned but encrypted) alternative of the JWT token.

Of the signature of JWT algorithms specified in the JSON Web Algorithms [RFC 7518], the following algorithm SHALL be supported:
- *HS256*: HMAC using SHA-256 hash algorithm.
- *RS256*: RSA using SHA-256 hash algorithm.

Other algorithms such as:
- *ES256*: ECDSA using P-256 curve and the SHA-256 hash algorithm ("ES256")

are RECOMMENDED. Other algorithms MAY be supported except the "NONE" that MUST NOT be used.

Note: 
- It is RECOMMENDED to use asymmetric (public-key based, e.g., RS256) methods for signing access token. When asymmetric methods are used, Resource Server do not need to store sensitive symmetric keys, making these methods more robust against malicious attacks.

#### 3.71.6.2 SAML Token

To use a SAML Bearer Assertion as an authorization grant, the Authorization Client SHALL perform the access token request with the value of the "grant_type" parameter set to "urn:ietf:params:oauth:grant-type:saml2-bearer" [RFC 7522, Section 2.1].

Authorization and Resource Server actors claiming conformance with the SAML Token Option shall comply with the *SAML 2.0 Profile for OAuth 2.0 Client Authentication and Authorization Grants* [RFC 7522] rules for issuing and using SAML 2.0 assertions as access token. The SAML 2.0 assertion content shall comply with XUA SAML assertion rules (see ITI TF-2b:3.40).

#### 3.71.6.3 Authorization Grant Scope

The scope parameter SHALL be used to restricting authorization grants to specific actions (e.g., restrict authorization to specific resources to read-only) and to convey claims, which are known to the Authorization Client only (e.g., if the user claims a breaking-the-glass access in a emergency situation). 

The value of the scope parameter SHALL be a collection of space-delimited, case-sensitive strings, whose values SHALL be defined by the Authorization Server [OAuth 2.1, Section 3.3].

User related scopes are RECOMMENDED to follow the syntax defined in *Health Relationship Trust Profile for Fast Healthcare Interoperability Resources (FHIR) OAuth 2.0 Scopes* [HEART scopes], i.e., it SHOULD be written as *user/resourceType.(read|write|\*)*, where 

- the *user* value SHOULD be *patient* if the current user is a patient, or *user* for healthcare professionals.

- the *resourceType* value SHOULD be the FHIR resource name (e.g., Patient, Observation, Appointment, a.s.o.).  

For example: 
- if a patient authorizes her device to read the Appointment resources to display them on her device, the scope granted SHOULD be *patient/Apointment.read*. 

- if a healthcare professional authorizes her web application or device to read and write Patient resources to be able to search, view and manage the patient data, the scope granted by the Authorization Server SHOULD be *user/Patient.\**.

- if a healthcare professional authorizes her web application or device to read all Patient data (incl. documents), the scope granted by the Authorization Server SHOULD to *user/\*.read*.

Note: The Authorization Server MAY ignore the scope requested by the Authorization Client or restrict it, based on the Authorization Server policy or the user's authorization grant. 

### 3.71.7 Expected Actions

### 3.71.7.1 Client Credential grant type

The Authorization Server SHALL authenticate the Authorization Client using it's client credential and respond with the access token as defined in Section 3.71.4 and 3.71.6 above. The Authorization Server SHALL verify the request. If the request is valid, the Authorization Server SHALL respond with the access token response conveying the access token in JWT or SAML 2.0 format as specified in Section 3.71.4 and 3.71.6 above.

### 3.71.7.2 Authorization Code grant type

The Authorization Server SHALL authenticate confidential and credential clients using the *client\_id* and *client\_secret*, or by other reliable client authentication method. In the latter case, the Authorization Server SHALL resolve the client authentication to a *client\_id* which was registered beforehand.     

The Authorization Server SHALL verify that all required parameters of the authorization request are present and valid. If valid, the Authorization Server SHALL authenticate the user and obtain the user consent (by presenting the user a form to authorize specific scopes or by establishing approval via other means). When the user consent is established, the Authorization Server SHALL issues an authorization code, access token and optional refresh token and direct the user-agent (e.g., browser) to the client redirect URI conveying the authorization code and client state value.

If the authorization request is invalid, the Authorization Server SHALL react as defined in [OAuth 2.1, Section 4.1.2.1]. 

The Authorization Client SHALL use the authorization code to request the access token from the Authorization Server. The Authorization Server SHALL verfiy the access token request as described in [OAuth 2.1, Section 4.1.3]. If the request is valid, the Authorization Server SHALL respond with the access token response conveying the access token in JWT or SAML 2.0 format as specified in Section 3.71.4 and 3.71.6 above. If invalid, the Authorization Server SHALL respond with an error as defined in [OAuth 2.1, Section 5.2].

### 3.71.8 Message Examples

The following is a non-normative example of JWT access token:

JOSE Header:
```
{
"typ": "IUA-JWT",
"alg": "HS256"
}
```

JWS Payload:
```
{
    "iss": "urn:tiani-spirit:sts",
    "sub": "b3ca1045-aa8b-42f9-9fd9-e0cbf5cb90a7",
    "aud": "http://ihe.connectathon.IUA/ResourceProvider-IHE-Connectathon",
    "exp": 1438251487,
    "nbf": 1438251187,
    "iat": 1438251187,
    "extensions" : {  
      "ihe_iua" : {  
        "subject_name": "Dr. John Smith",
        "subject_organization": "Central Hospital",
        "subject_organization_id": "urn:oid:1.2.3.4",
        "home_community_id": "urn:oid:1.2.3.4.5.6.7.8",
        "resource_id": "urn:uuid:1.2.3.4",
        "subject_role": [
          {
            "system": "2.16.840.1.113883.6.1",
            "code": "28570-0",
            "display": "ProcedureNote"
          }
        ],
        "purpose_of_use": [
          {
            "system": "2.16.840.1.113883.6.2",
            "code": "99-0",
            "display": "Social Worker"
          }
        ]
      }
    }
}
```

### 3.71.9 Security Considerations

Authorization Client and Authorization Server claiming compliance with this profile SHALL fufill the security requirements defined in the OAuth Authorization Framework [OAuth 2.1], especially: 

- All HTTP transaction must be secured by using TLS or equivalent transport security.

- Authorization Clients SHALL verify the identity of the Authorization Server, either by validating the TLS certificate chain or by other reliable methods. 

- Authorization codes SHALL be for single use and short-lived with a lifetime less or equal to 5 minutes. 

- Access token SHALL be short-lived with a lifetime of 1 hour or less. A lifetime less or equal to 5 minutes is RECOMMENDED. 

- Refresh token MAY be long lived. 

- To reduce the attack surface, client claims and authorization grants SHALL be the minimal. I.e., the authorizatiom grant scope requested by the Authorization Client shall be the minimal required scope for the resource request to be used for.          


#### 3.71.9.1 Security Audit Considerations

Authorization Servers SHOULD produce an audit record for any failed attempt to obtain authorization. IHE does not specify the format of audit records for authorization servers.

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




**Add Section 3.72**

## 3.72 Incorporate Authorization Token

### 3.72.1 Scope

This transaction is used to incorporate authorization information to HTTP RESTful transactions. 


### 3.72.2 Use Case Roles

Table 3.72.2-1: Actor Roles

|Actor                |Role
|------------         |-------------------------------------------------------------
| Authorization Client| Authorization component of a HTTP RESTful transaction client.
| Resource Server     | Authorization component of a HTTP RESTful transaction server.


### 3.72.3 Referenced Standards

This transaction relies on standards defined in the following documents and the references therein: 

- *OAuth 2.1*: The OAuth 2.1 Authorization Framework, published as draft-ietf-oauth-v2-1-00. July 2020.

- *JWT Access Token*: JSON Web Token (JWT) Profile for OAuth 2.0 Access Tokens, published as draft-ietf-oauth-access-token-jwt-07, April 2020.

- *RFC 7522*: SAML 2.0 Profile for OAuth 2.0 Client Authentication and Authorization Grants, May 2015. 


#### 3.72.3.1 Related IHE Profiles

XUA Cross-Enterprise User Assertion -- Attribute Extension

### 3.72.4 Interaction Diagram

![simple-iauth](./media/basic-flow.png)

Figure 3.72.4-1: Process flow for Incorporate Authorization Token
Transaction

```
\@startuml  
group Get Authorization Token \[ITI-71\]   
AuthorizationClient -\> AuthorizationServer : Authorization Request  
AuthorizationClient \<- AuthorizationServer : Authorization Response \+ Authorization Token  
end  
group Incorporate Authorization Token \[ITI-72\]  
AuthorizationClient -\> ResourceServer : Resource Request + Authorization Token  
AuthorizationClient \<- ResourceServer : Resource Response  
end  
\@enduml
```

Main Flow:

1.  The Authorization Client actor sends a resource request to a Resource Server, together with the access token. The access token may be a JWT token or a XUA compliant SAML 2.0 Assertion.

2.  The Resource Server makes an access control decision based upon the information from the access token and the transaction details. It may provide access to the resource, a subset of the resource, or reject the request in total.

This transaction works in conjunction with other HTTP RESTful transaction. It extends the transaction by adding information to the HTTP request for that HTTP RESTful transaction.

### 3.72.5 Trigger Events

A client needs to make an HTTP RESTful transaction to a Resource Server that enforces access authorization.

### 3.72.6 Message Semantics

The Authorization Client SHALL incorporate the access token in the authorization header of the HTTP request.

#### 3.72.6.1 JSON Web Token Option

An Authorization Client that claims the JSON Web Token Option SHALL be able to incorporate a JWT as access token defined in Section 3.71.6.3 in the HTTP Basic Authorization header. A Resource Server that supports the JSON Web Token Option SHALL be able to accept and understand a JWT token as defined in Section 3.71.6.3.

#### 3.72.6.2 SAML Token Option

An Authorization Client that supports the SAML Token Option SHALL be able to incorporate a XUA compliant SAML 2.0 Assertion (see ITI TF-2b: 3.40.4.1.2 Message Semantics) as access token. The SAML assertion shall be encoded as specified in Security Assertion Markup Language (SAML) 2.0 Profile for OAuth 2.0 Client Authentication and Authorization Grants [RFC 7522, Section 2.1] rules and included in the HTTP Basic Authorization header with type *IHE-SAML*.

A Resource Server that supports the SAML Token Option SHALL be able to accept and understand a SAML assertion that complies with the XUA specification as the access token for requests.

### 3.72.7 Expected Actions

The Authorization Client SHALL incorporate the access token to Resource Server requests in the HTTP Basic Authorization header. 

The Resource Server SHALL validate the access token and ensure that it has not expired. The Resource Server SHALL verify, that the claims conveyed in the access token match the transaction type and data (E.g., verify that the patient_id attribute of the access token corresponds to the patient_id of the resource request). 

If the authorization grant scope is restricted, the Resource Server SHALL verify, that the scope covers the transaction to the requested resource [OAuth 2.1, Section 7]. 

In addition, the Resource Server SHALL enforce the access policies set in the specific environment by matching the information from the access token and the transaction data to the access policies.
 
If the token verification, scope matching or the access policy enforcement fails, the Resource Server SHALL respond a HTTP 401 (Unauthorized) error.

### 3.72.8 Message examples

#### 3.72.8.1 JSON Web Token Option

A non normative example of the access token incorporation to a RESTful transaction is as follows: 

```
GET /example/url/to/resource/location 
HTTP/1.1
Authorization: IHE-SAML fFBGRNJru1FQd\[...omitted for brevity...\]44AzqT3Zg
Host: examplehost.com
```

#### 3.72.8.2 SAML Token Option

A non normative example of the access token incorporation to a RESTful transaction is as follows: 

```
GET /example/url/to/resource/location 
HTTP/1.1
Authorization: IHE-SAML fFBGRNJru1FQd\[...omitted for brevity...\]44AzqT3Zg
Host: examplehost.com
```

### 3.72.9 Security Considerations

Authorization Client and Resource Server claiming compliance with this profile SHALL fufill the security requirements defined in the OAuth Authorization Framework [OAuth 2.1], especially: 

- All HTTP transaction must be secured by using TLS or equivalent transport security.

- Authorization Clients SHALL verify the identity of the Resource Server when making requests to protected resources, either by validating the TLS certificate chain [OAuth 2.1, Section 7.4.2] or by other reliable methods. 

#### 3.72.9.1 Security Audit Considerations

When an ATNA Audit message needs to be generated by the Resource Server and the user is authenticated by way of a JWT Token, the ATNA Audit message **UserName** element shall record the JWT Token information using the following encoding:

**alias\"\<\"user\"@\"issuer\"\>\"**

where:
-   **alias** SHALL match the JWT token's "aud" parameter
-   **user** SHALL match the JWT token's "sub" parameter
-   **issuer** SHALL match the JWT token's "iss" parameter

When an ATNA Audit message needs to be generated by the Resource Server and the user is authenticated by way of a SAML Token, the ATNA Audit message **UserName** element shall record the SAML token information using the following encoding:

**alias\"\<\"user\"@\"issuer\"\>\"**

where:
-   **alias** SHALL match the optional string within the SAML Assertion\'s Subject element SPProvidedID attribute
-   **user** SHALL macth the required content of the SAML Assertion\'s Subject element
-   **issuer** SHALL match the X-Assertion Provider entity ID contained with the content of SAML Assertion\'s Issuer element
