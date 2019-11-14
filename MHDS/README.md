This profile will be a rather small amount of text, mostly Volume 1. This will mostly orchestrate many other profiles into an HIE infrastructure.   This cloud of HIE infrastructure will be made up of many existing actors and some new actor(s) that have some business functionality discussed below. 

# Central HIE Infrastructure 
The central HIE infrastructure might be a virtual cloud of the existing profile specific actors to enable modularity. Modularity where each function could be provided by different vendors, possibly different vendors providing different instances of the same actor. Trying to leverage as much as possible on reference implementations of FHIR Server, and also leverage as much as possible of modularity enabled by defined interoperability interfaces (IHE Profiles). Possibly for those that desire it, ONE common-use FHIR server (e.g. HAPI server, FIRELY server, etc) could serve as the whole central HIE Infrastructure. 

# Business functions
The first step is to identify all the additional requirements that an HIE infrastructure would need beyond those already found in MHD. That is similar to the requirements that the XDS Registry and XDS Repository have that will need to be imposed upon an MHD based central infrastructure. So far I have:

* Persistence of Document, DocumentManifest, List, and DocumentReference
    * ability to transform FHIR xml <--> json for these three resources 
* Subscribe or be configured as an endpoint of the PRIM patient feed -- Update metadata when Merge occurs
    * Update DocumentReference.subject, DocumentManifest.subject, and List.subject 
	* Update DocumentReference.author, List.source, DocumentManifest.recipient 
* Seems the PRIM manager should be part of the central infrastructure. So that clients can use PDQm, PIXm, or PRIM feed to be up-to-date on patient identity. Right?
* Management of metadata rules, and verification of new submissions meet those rules -- This is the set of allowed metadata as we describe in the Metadata Handbook
    * might bring in the SVSm for this?  Seems it would be good to have this right away 
* Organization directory ? -- should mCSD be a requirement or recommendation? What specific value are we looking for?
	* discovery of MHD endpoints given a Organization as discovered using mCSD
	* can also be used to validate Practitioner, PractitonerRole, Organization, etc... as used in the documentReference metadata.
* Security -- 
    * mandatory use of ATNA fhir flavors -- consistency with XDS  
    * Recommendation for use of IUA? Or should this be mandated with operational allowance for other client side security to be used? 
* Privacy - ??? We don't have any privacy demanded in XDS, and we don't yet have Consent covered in IHE profiles.
	* do we just impose this at the business rule level?
	* do we kickoff a project to create FHIR Consent function?
* Is there reason to add FHIR Provenance Resource to the infrastructure? 
	* on Source of data, The Provenance resource seems redundant given that DocumentReference and DocumentManifest cover this function already.
	* only obvious gap is as published by a Registry on a query to indicate that the results returned by the Registry is published at that time by the Recommendation. Is this important or not?
	* possibly when federating communities as Provenance from each community 'registry'
* Is the function of QEDm server a useful option? Not mandated, but declared option?
    * some have discussed an actor that pulls FHIR Resources (element level) and produces a FHIR Document that gets registered. This seems interesting, but not clearly needs driven 
* different rules than XDS-on-FHIR ?
	* such as not using contained resources for author and authenticator  - so that they align with mCDS registry.
		* This would only work if the mCSD service was also part of the HIE infrastructure mandate AND that infrastructure maintained versioned resources. So that DocumentEntry.author then would hold a VERSION specific url. 
			* which brings up maintenance of mCSD resource considerations
	* clearly source must still be contained. right? -- or can this also be versioned instances of Patient from the PRIM infrastructure.
* I was not expecting to have two actors like XDS to represent Registry and Repository. This is possible, but I am not hearing from the target audience that they desire this. I don't want to impose this architecture if it is not clearly within the environmental need of the target. Yes I understand that XDS has this architecture, but just because XDS has it does not mean that the MHD-HIE must have it. 
	* I want to be needs driven, not perceived architecture driven.  
	* I suspect we will learn in Trial-Implementation if this simplifiying architecture is correct.
	* However I think our target environment does have larger organizations that might want repository function local

Any other items?

# Agenda

## October 28, 2019
* Review current document -- not much has been done
* Review [diagram](https://www.websequencediagrams.com/?lz=dGl0bGUgRkhJUiBNSEQgQ29udHJvbGxlZCBFeGNoYW5nZSAoMTAwJQAeBSkKCnBhcnRpY2lwYW50IFNvdXJjZQAGDVBhdGllbnQAGg1NUEkAKg1DQQA5DURpcmVjdG9yeQBPDUF1ZGl0IFJlcG8AZg1WYWx1ZVNlAAcTUmVnaXN0ADcPUmVjaXAAgQwFCm5vdGUgb3ZlciBDQSAKQWxsIChBVE5BKSBzeXN0ZW0gCmFuZCBvcmcgaWRlbnRpdGllcwpjaGFpbmVkIGhlcmUuCj8_PwplbmQgbm90ZQBEDACBNwpPbmx5AIEACSBhbmQgCgCBPgogCmVuZHBvaW50cyBuZWVkIApwdWJsaXNoAFoHAEcZAIIAC0FsbCBzZWN1cml0eQCBLAVwcml2YWN5CmV2ZW50cyBhcmUgCmxvZ2cATAgAgRwUAII2Dk1hbmFnZW1lbnQgb2YKY29tbW9uIHYAgmAHcwppbmNsdWRpbmcAglcKZW5mb3JjZWQgTWV0YWRhdGEKKG0AAwcgaGFuZGJvb2spAIIfC29wAIQPCQCCVQh5IChQUklNIGZlZWQpCgCELgctPgCESwY6IHZpc2l0cyBzAIRaBgCEYQYtPk1QSTogdXBkYXRlAEcJSQBJBwpNUEkAGwdjcm9zcy1yZWZlcmVuY2UgdG8gR29sZGVuIFBJRAAiBgCEJAgARgkAFgtlbmQAgS0GAIMXByBuZXcgZG9jdQCCHgUoTUhEKQCBBA5kaXNjAIRTBQBcCiAoUElYbSkAhG4GcmlnaHQgb2YAhicIa2VlcABHCmEAhj4JaS5lLgCGfwVQcm92aWRlAIQ7BQCFUAZlciB3aXRoIG5vIEJpbmFyeSwgCmJ1dCAuYXR0YWNobWVudC51cmwgdG8Ahw0HIHNlcnZpYwCDdgogAII9CQCBcgoAgVkITmV3IEQAgVkIUgCCLwkoTUhEIHAAgQYGAINKBQCDRAYAgWYJcACDTAcAgWYGAIVpBQCDfgUAgh0GAINLCQCGegkAg04JcgCHDAkAhxYJAIM_HgCEIA0Ag0EoAEwQAIMOGSBxdWVyeSkAgQEMKwCEFwoAg1YIeSBFbnRyeShzKQCCEwYALAkAiHAGLT4tAIFeC2hlcmUAhwcFACwIAFANAIVeCEFzayBmb3IAgiwKIHJldHJpZXZlAIRYCisAikoHOiBpcyB0aGlzAIlJCiBhdXRob3JpemVkAEIFABkFZGF0YT8AhGkPAIsMCGxpa2VseSBpbnRlbmEAhCILCmNvdWxkIGIAjAAHQ29uc2VudCAKb3IgSEVBUlQAiWsKAIcgCS0AhyIIeWVzAIcXCQCBdgxIAIF6CACIGwUAhk8FAIp3CgCLDAoAgUMKbQCGIQVtYWtlCnRoZQCGZwptb3JlCmFjY2Vzc2libGUgbGlrZSAKdGhyb3VnaCBtWERFL1FFRG0AhV4LCg&s=rose)
* Establish how much of the HIE whitepaper and handbook should be duplicated within
* Establish a security model to deal with federation