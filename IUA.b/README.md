# IUA work item

Improve IUA based on lessons-learned

## Working Process

* Bi-Weekly meeting on ititech calendar
* Ballot plan for two phase ballot. First to be minimal corrections where there is problems. Second to focus on new features or more involved clarifications.
* using github issues for all changes big or small
* using kanban board for managing tasks https://github.com/IHE/IT-Infrastructure/projects/1
  * two columns for in progress (discussion vs editing) - where issues in editing state are agreed on what the edit should be, discussion is for consensus building.
* Editors will edit the markdown (we no longer maintain the WORD docx)
* Editors will create pull-requests, include issue being closed, and assign to John, Walco, and Martin for review of the pull-request. Three approvals will merge automatically. Anyone can request it be further reviewed on bi-weekly call


## Breaking changes

* Reworked the Use Cases section and added decriptions of the use cases from the user perspective.

* Reworked the text descriptions to establish the borders between authentication, authorization and policy enforcement. 

* Established options to the Get Authorization Token transaction to distinguish authorization code and client credential flow.

* Added support for OAuth public clients and aligned the profile with the latest OAuth 2.1 draft specification.

* Established UDAP extensions to improve the structure of JWT and reworked the examples.  

* Replacement of the "Bearer" option with "Token Introspection" option. This option utilizes OAuth2 Introspect (RFC 7662). This option allows Resources Servers to deal with any token format (JWT/SAML/other) by obtaining the claims associated with an access token through an introspect API offered by the Authorization Server.

* Removal of hard requirement for JWT formatted access token support. JWT, SAML and Introspect have all become optional. Resource and Authorization Servers need to implement at least one.

* The IHE-JWT and IHE-SAML HTTP Authorization schemes have been replaced by the "Bearer" scheme to be compatible with RFC 6750. All token formats are now treated as bearer tokens. The Authorization Client does no longer need to be aware of the token format.

* The "audience" claim associated to an access token can now be a JSON array of server identifiers. Resource Servers still MUST check their presence in the audience claim.

* Custom claim names have been replaced by established JWT (Access Token) RFC claims whenever possible and aligned with the UDAP extensions mechanism.

## Open questions

* The addendum contains a section on IHE-MHD to indicate authorization scope specification and usage. MHD is used as example case, extendable to other profiles that employ RESTful APIs. Open question is how the profile specific authorization scopes should be specified, and if, when an how they should relate to HEART/SmartOnFHIR scopes.

## Other changes

* Aligned the profile with the latest standards such as OAuth 2.1, OpenId Connect, JWT, OAuth2 Introspect.

* Resource field in token request has become optional for client, should be supported by authorization server.

* Removal of references to FHIR/Heart scopes. IUA is now scope definition agnostic. Scopes to be added to REST/FHIR based IHE profiles.

* Introduction of option for OAuth2 Authorization Server Metadata (RFC8414). The metadata document contains references to endpoint locations, signing key material, and an indication of the issued token format.

* Updates to support service-to-service authorization schemes (eg., by removing strong dependencies on user consent).

* Improved profiling of OAuth2 interactions providing clarity on request/response data requirements and semantics.

* Support for alternative authorization grants (e.g. client jwt_grants). Not mandatory to be supported by an Authorization Server
