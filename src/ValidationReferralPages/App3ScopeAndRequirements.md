### Scope Overview
This BaRS Application (application 5) covers only use cases:
* GP to Pharmacy CPCS (Community Pharmacist Consultation Service) for Minor Illness Service

The payloads and workflow have been designed to support these services. Other {{pagelink:applications, text:BaRS Applications}} offer scope for alternative use cases.

### Functional Scope
**Service Discovery**
* Establishing a service to direct requests to is a mandatory step in the workflow
* There is no restriction on the service discovery tools used. Any are capable of being supported whether national or proprietary
* The service **must** be configured within the BaRS infrastructure (Endpoint Catalogue) before requests can be made 

**Referral**
* A referral is a request for care on behalf of an individual from one service to another 
* The referral can be sent without having to establish the capacity the service offers
* The referral will contain primarily clinical information, indicating the need of the individual and **must** state the anticipated action required by the Receiving service (Task)

**API-M**
* All requests and response associated with BaRS must occur through the BaRS API Proxy

**Constraints**
* All Service IDs in First of Type (FoT) will be those of Urgent and Emergency Care (UEC) Directory of Services (DoS) 
* No guidance provided on display of referral information beyond the {{pagelink:principles_prerequesites, text:Principles for rendering BaRS Payload}}.
* Consent within BaRS will be for Direct-Care only 
* Certificates for Receiving messages to use nhs.uk domains only and internet facing 
* Clincial Constraints exist - See Hazard Log
* No element level 'updates' to requests are supported. A new request must be generated to change information in the referral request


### Requirements

**Service Discovery** 
* The service **must** support a unique identifier which the Sender extracts to engage in the BaRS referral workflow

**Referral** 
* Clinical and non-clinical users **must** be capable of making referrals
* The referral Receiver **must** accept the referral request regardless of whether the patient is known to the service provider
* The referral Receiver **must** accept potential patients who do **<ins>not</ins>** have a national validated identifier e.g. NHS Number.
* Where a national identifier is included, it **must** be 'Number present and verified', otherwise, the referral Sender **must <ins>not</ins>** include in the request
* Any new or existing safeguarding concern, recorded as part of the assessment, **must** be included in the referral Sender's request
* The referral Receiver **must** clearly identify any included safeguarding concern to the end user
* Any new or existing individual requirements e.g. need for interpreter, recorded as part of the assessment, **must** be included in the referral Sender's request
* The referral Receiver **must** clearly identify any included individual requirements to the end user
* The referral Receiver **must** accurately represent information made by the Sender to the end user 
* The referral Sender **must** include the Pharmacy Service the request is intended for from the defined list ~~include reference to this~~
* The referral Sender **must** indicate consent obtained to share to the Receiver 
* The referral Sender **must** indicate the urgency (providing timeframe within which included actions are expected to take place) of the request to the Receiver 
* The referral Sender **must** make available the human readable identifier for the referral, included in the HTTP synchronous response, to the end user
* Where the referral was <ins>not</ins> successful, the Receiver **must** send an appropriate response
* Where the referral was <ins>not</ins> successful, the Sender **must** present an appropriate message to the end user
* Update to amend a referral request is <ins>not</ins> supported. If a referral Sender wishes to change information in a request they **must** follow the re-refer workflow

**Cancel referral** 
*	The referral Sender **must** be capable of cancelling any referral made by them, within the current consultation or after the consultation event
*	The referral Sender **must** retrieve the referral to be cancelled, from the referral Receiver, prior to cancellation to ensure they are working with the most up-to date version and it has not already been completed
*	The referral Sender **must** provide visible confirmation to the end user of the status returned by the referral Receiver, i.e. whether the original referral was successfully cancelled or not
*	If the update fails the referral Receiver **must** respond with the most appropriately aligned error 
*	The referral Receiver **must** store all previous versions of the referral
*	The referral Receiver **must <ins>not</ins>** be required to inform the patient of the cancellation of the referral.  Business/clinical responsibility for informing the patient remains with the referral Sender

**Re-refer** 
*	The referral Sender **must** be capable of re-referring within the current consultation or after the consultation event
*	If a callback occurs, after the consultation has been completed, prior to attempting a re-refer the patient **should** be reassessed 
*	The referral Sender **should** revoke the original referral prior to making a re-referral, whether within the current consultation or after the consultation event
*	The referral Sender **must** provide visible confirmation to the end user of the status returned by the Receiver, i.e. whether the original referral was successfully revoked and the new referral made 
*	The referral Receiver **must <ins>not</ins>** be required to inform the patient of the cancellation, incurred as part of the re-refer process.  Business/clinical responsibility for informing the patient remains with the referral Sender

**Contacts** 
* A minimum of one contact (patient or third party) with a contact method (phone, email, etc.) of <ins>phone</ins> **must** be provided in referral requests
* All contacts **must** have a rank associated with them
* There **must** be only one contact with a rank of 1
* All contacts **must** have at least one contact method (phone, email, etc.)
* All contact methods **must** have a rank
* There **must** be only one contact method with a rank of 1
* The contact ranked 1 and the contact method ranked 1 **must** be the primary callback for the request

**Caching**
* The local caching of retrieved metadata (Capability Statements and Message Definitions) requests is permitted to improve performance
* Caching of responses **must <ins>not</ins>** exceed 24 hours (12 hours is recommended)
* There **must** be a mechanism to manually clear the cache