This profile only a Volume 1, as it orchestrates other profiles into an HIE infrastructure.   This cloud of HIE infrastructure is be made up of many existing actors and one new actor(s) that have some business functionality discussed below. 

# Central HIE Infrastructure 
The central HIE infrastructure might be a virtual cloud of the existing profile specific actors to enable modularity. Modularity where each function could be provided by different vendors, possibly different vendors providing different instances of the same actor. Trying to leverage as much as possible on reference implementations of FHIR Server, and also leverage as much as possible of modularity enabled by defined interoperability interfaces (IHE Profiles). Possibly for those that desire it, ONE common-use FHIR server (e.g. HAPI server, FIRELY server, etc) could serve as the whole central HIE Infrastructure. 

MHDS does include mXDE informatively as it is a bridge that is compatible with MHDS, but there is no specific requirements.

# Plan
May 2020 virtual face-to-face to resolve public comment and release for Trial Implementation.
* March 2020 comment resolution spreadsheet contained in github 

# Open Issues

1. Given that this profile audience is likely to include those new to IHE Document Sharing exchange, there is more detail included in this supplement in order to be more self-contained and not rely on the reader referencing other whitepapers and handbooks. The section X.7 could be considered to be removed if and when the ITI whitepaper on using IHE Profiles for and HIE is updated to include MHD and MHDS.