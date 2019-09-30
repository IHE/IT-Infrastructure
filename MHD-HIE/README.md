This profile will be a rather small amount of text, mostly Volume 1. This will mostly orchestrate many other profiles into a HIE. It will create a new central actor that has additional business rules as necessary.

The first step is to identify all the additional requirements that an HIE infrastructure would need beyond those already found in MHD. That is similar to the requirements that the XDS Registry and XDS Repository have that will need to be imposed upon an MHD based central infrastructure. So far I have:

* Persistence of Document, DocumentManifest, List, and DocumentReference
** ability to transform FHIR xml <--> json for these three resources
* Subscribe or be configured as an endpoint of the PRIM patient feed
** Update DocumentReference.subject, DocumentManifest.subject, and List.subject when a Merge occurs
* Seems the PRIM manager should be part of the central infrastructure. So that clients can use PDQm, PIXm, or PRIM feed to be up-to-date on patient identity. Right?
* Management of metadata rules, and verification of new submissions meet those rules -- This is the set of allowed metadata as we describe in the Metadata Handbook
** might bring in the SVSm for this?  Seems it would be good to have this right away
* Organization directory ? -- should mCSD be a requirement or recommendation? What specific value are we looking for?
* Security -- 
** mandatory use of ATNA fhir flavors -- consistency with XDS 
** Recommendation for use of IUA? Or should this be mandated with operational allowance for other client side security to be used?
* Privacy - ??? We don't have any privacy demanded in XDS, and we don't yet have Consent covered in IHE profiles.
* Is there reason to add FHIR Provenance? It seems redundant given that DocumentReference and DocumentManifest cover this function already.
* Is the function of QEDm server a useful option? Not mandated, but declared option?
** some have discussed an actor that pulls FHIR Resources (element level) and produces a FHIR Document that gets registered. This seems interesting, but not clearly needs driven

I was not expecting to have two actors like XDS to represent Registry and Repository. This is possible, but I am not hearing from the target audience that they desire this. I don't want to impose this architecture if it is not clearly within the environmental need of the target. Yes I understand that XDS has this architecture, but just because XDS has it does not mean that the MHD-HIE must have it. I want to be needs driven, not perceived architecture driven.  I suspect we will learn in Trial-Implementation if this simplifiying architecture is correct.

Any other items?