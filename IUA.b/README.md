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

 * The IHE-JWT Authorization scheme has been replaced by the "Bearer" to be compatible with RFC 6750  
 * Custom claim names have been replaced by an established OpenID claim whenever possible and aligned with the UDAP extensions mechanism 

## Open questions

 * Do we want to require OpenID Connect as a base for deployment and security options?

## Other changes

 * Aligned the profile with OpenID Connect and the use of published OAuth RFCs.
