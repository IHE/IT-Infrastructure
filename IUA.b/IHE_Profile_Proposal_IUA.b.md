IHE Work Item Proposal (Short)

Proposed Work Item: IUA.b
=========================

> Proposal Editor: Walco van Loon
>
> Work item Editor: Walco van Loon (supported by Massimiliano Masi and
> John Moehrke)
>
> Date: 9 June 2019
>
> Version: 0.1
>
> Domain: ITI

The Problem
===========

> Since its initial publication in 2015, IUA started out with a few
> incompatibilities with base standards. Additionally, since then, OAuth
> 2.0 and related authentication frameworks (OpenID Connect,
> SMARTonFHIR) have matured. IUA still fills a void within these
> specifications and thus deserves an update. This work item replaces
> the following CPs that have been opened over the years:

-   **CP-ITI-907 - IUA Maintenance and alignment with FHIR initiatives**

-   CP-ITI-1166 - IUA - update to token specification

-   CP-ITI-1149 - IUA - improve JWT token extension claim names

> 17 companies have tested IUA over the years at Connectathons. Many of
> the vendors have experienced the issues recorded in the CPs during
> testing. Besides these issues, each of these vendors will run into
> additional integration issues when they need to connect to HL7 FHIR
> SMART enabled systems. Conversly, IHE unaware SMARTonFHIR enabled
> clients can not integrate with MHD enabled HIEs. These integration
> issues are causing delays in project delivery and result in higher
> costs due to the need for custom integration software. This impact is
> even expected to grow with the rise of popularity of REST based
> interaction.

Key Use Case {#key-use-case .ListParagraph}
============

> Same as for IUA; citing from IUA Vol 1: "the IUA Profile adds
> authorization information to HTTP RESTful transactions. The IUA actors
> and behavior will be added to other profiles and transactions that
> need authorization."

Standards & Systems
===================

> Same as for IUA with some updates. Probably the new IUA profile will
> be more explicitly based on OpenID Connect.

Discussion
==========

> IHE developed the original IUA Profile. Action is needed: it either
> has to be updated or withdrawn.
