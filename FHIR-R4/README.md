This Public Comment ballot contains a subset of IHE profiles that leverage FHIR. The subset is made up of a high priority set of IHE Profiles that cover the functionality defined in USA HHS/ONC Meaningful Use regulations around the need for an API. The trigger for this Public Comment ballot is to update these profiles from FHIR STU3, to FHIR R4. The changes made to the supplements is targetting this FHIR Release 4 update. There are other improvements that were identified as part of the revision and from Change Proposal submissions. Where these other improvements are non-controversal they are included in this Public Comment. Where these improvement opportunites require discussion or may present concerns with passage of the Public Comment ballot, they will be addressed as part of standalone Change Proposals. This approach is intended to better aid with a successful Public Comment ballot so as to have higher likelyhood of being able to meet a March 1st publication timeframe.


Ballot comment disposition
* During the week of February 25, 2019 comments will be resolved using https://docs.google.com/spreadsheets/d/1G3kimc_j3TOLx1dv03l_C0ymmGGfUFFlq73qKKKLkVw/edit?usp=sharing

Summary of Changes:

The FHIR specification changed in response to public comment based on ballot and experience. For details on the summary of changes of the FHIR specification between STU3 and R4 please see http://build.fhir.org/history.html

The IHE profiles of PDQm, MHD, QEDm, mCSD, and the Appendix Z were updated to reference FHIR R4. The changes were dominantly simply to reference FHIR R4 rather than FHIR STU3. Thus the most important changes to implementations are found in the FHIR specification changes. Some changes were also initiated by a Change Proposal that identified a mistake in the STU3 version of the profile. Some changes were open-issues in STU3 that are now fixed in the FHIR R4 core specification. Change Proposals and open-issues are noted in the closed-issues in these drafts. These versions of the supplement were in Public Comment that resulted in 88 public comments that were then resolved. Note that mXDE profile is independent of the FHIR revision, as it orchestrates MHD and QEDm.

The following are specific additional changes beyond the update to reference FHIR R4:
* MHD - now requires Document Recipient declaring XDS on FHIR Option must support all XDS association types
* MHD - the canonical URI used for profiles are available, but they have not yet been created. These StructureDefinition xml files will be made available later as they are not normative.
* MHD - the canonical URI used for the Provide Document Bundle transaction has changed because the FHIR canonical URI encoding rules don't allow for "-" character. We could have just change ITI-65 into ITI_65, but a breaking change is a breaking change. So we chose to replace with an actual structure definition based in the same URI space as our other Structure definitions. This means that we would no-longer use http://ihe.net/fhir/tag/iti-65, but rather we would use http://ihe.net/fhir/StructureDefinition/IHE_MHD_Provide_Comprehensive_DocumentBundle, or http://ihe.net/fhir/StructureDefinition/IHE_MHD_Provide_Minimal_DocumentBundle
* MHD - many updates to the XDS-FHIR mapping, including recognizing the use of the .meta element to support minimal metadata
* MHD - recognition of ProviderRole use
* QEDm - fixed a coding issue in Provenance.agent.role, to use Provenance.agent.type. More specific on the system, and corrected to use 'assembler'
