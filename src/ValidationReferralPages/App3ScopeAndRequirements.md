---
topic: APP3-ScopeAndRequirements
---

 <div markdown="span" class="alert alert-warning" role="alert"><i class="fa fa-warning"></i><b> Important:</b> This Application is currently under development <hr><p> This is a preview of a developing documentation for information only. It is not intended to be used until the completed v1.0.0 Application is released<p> If you are interested in developing a BaRS compliant solution for these use cases right now, please use the contact form <a href="https://digital.nhs.uk/services/booking-and-referral-standard/enquiry-form" target="_blank">here</a> and the team will be in touch</div>


## {{Referrals into CAS (Application 3)}}

### Use cases supported


This application supports the following use case:
* 999 Ambulance Service Trust (AST) referral to Clinical Assessment Service (CAS)

Note: for 999 AST validation requests to CAS, that require a response please see {{pagelink:LINK TO APP4 TO BE ADDED}}

### Data model endorsements

The referral information data model is based on user research with NHS 111 service providers, 999 Ambulance Service Trusts, Clinical Assessment Services and clinical and administrative Emergency Department staff.  We carried out this research in parallel with the [Professional Records Standards Body (PRSB)](https://theprsb.org/) who examined the wider brief of 'referrals from NHS 111 to any other care setting' 

For the Referral into a CAS from a 999 AST use case, the data model was endorsed by NHS England following consultation with the [Association of Ambulance Chief Executives (AACE)](https://aace.org.uk/),  National Ambulance Information Group (NAIG), National Ambulance Services Medical Directors' Group (NASMeD) and National Ambulance Digital Leaders Group (NADLG)
### Functional Scope

**Service Discovery**

* Establishing a service to direct requests to is a mandatory step in the workflow
* There is no restriction on the service discovery tools used. Any are capable of being supported whether national or proprietary
* The service **must** be configured within the BaRS infrastructure (Endpoint Catalogue) before requests can be made 

**Referral**
* A referral is a request for care on behalf of an individual from one service to another 
* The referral can be sent without having to establish the capacity the service offers
* The referral will contain primarily clinical information, indicating the need of the individual and **should** state the anticipated action required by the Receiving service
* Supporting information, other than the assessment, is expected to be included in a referral, if collected, including:
    * new or existing safeguarding concerns
    * locally held Special Patient Notes
    * external information sources used during initial assessment prior to referral
    * scene safety information
    * timing information to support the timely delivery of care and reporting

**API-M**
* All requests and response associated with BaRS must occur through the BaRS API Proxy

**Constraints**
* Supporting use of Emergency Call Prioritisation Advisory Group (ECPAG) approved  Clinical Decision Support Systems only (NHS Pathways, NHS Pathways Clinical Content Support (PaCCS) and Advanced Medical Priority Dispatch System (AMPDS)).
* All Service IDs in First of Type (FoT) will be those of Urgent and Emergency Care (UEC) Directory of Services (DoS) 
* No guidance provided on display of referral information beyond the {{pagelink:principles_prerequesites, text:Principles for rendering BaRS Payload}}.
* Consent within BaRS will be for Direct-Care only 
* Certificates for Receiving messages to use nhs.uk domains only and internet facing 
* Clincial Constraints exist - See Hazard Log

### Requirements

**Service Discovery** 
* The service **must** support a unique identifier which the Sender extracts to engage in booking and referral workflows

**Referral Request**
* The referral Receiver **must** accept the referral request regardless of whether the patient is known to the service provider
* The referral Receiver **must** accept potential patients who do **<ins>not</ins>** have a national validated identifier e.g. NHS Number.
* The referral Sender **must** must send incident location information as part of their request
* The referral Sender **must** must send scene safety information as part of their request
* Any new or existing safeguarding concern, recorded as part of the assessment, **must** be included in the referral Sender's request
* The referral Receiver **must** clearly identify any included safeguarding concern to the end user
* The referral Receiver **must** accurately represent information made by the Sender to the end user
* The referral Sender **must** make available the human readable identifier for the referral, included in the HTTP synchronous response, to the end user
* Where the referral was <ins>not</ins> successful, the Receiver **must** send an appropriate response
* Where the referral was <ins>not</ins> successful, the Sender **must** present an appropriate message to the end user

**Update referral**
*	The referral Sender **must** be capable of updating any referral made by them, within the current consultation or after the consultation event
*	The referral Sender **must** retrieve the referral to be updated from the referral Receiver prior to cancellation to ensure they are working with the most up-to date version and it has not already been completed
*	The referral Sender **must** provide visible confirmation to the end user of the status returned by the referral Receiver, i.e. whether the original referral was successfully updated or not
*	If the update fails the referral Receiver **must** respond with the most appropriately aligned error 
*	The referral Receiver **must** store all previous versions of the referral
*	The referral Receiver **must <ins>not</ins>** be required to inform the patient of the updating of the referral.  Business/clinical responsibility for informing the patient must remain with the referral Sender


**Cancel referral** 
*	The referral Sender **must** be capable of cancelling any referral made by them, within the current consultation or after the consultation event
*	The referral Sender **must** retrieve the referral to be cancelled from the referral Receiver prior to cancellation to ensure they are working with the most up-to date version and it has not already been completed
*	The referral Sender **must** provide visible confirmation to the end user of the status returned by the referral Receiver, i.e. whether the original referral was successfully cancelled or not
*	If the update fails the referral Receiver **must** respond with the most appropriately aligned error 
*	The referral Receiver **must** store all previous versions of the referral
*	The referral Receiver **must <ins>not</ins>** be required to inform the patient of the cancellation of the referral.  Business/clinical responsibility for informing the patient must remain with the referral Sender


**Incident Location**
*  The Sender  **must** include the incident location in the referral request
*  All Locations **must** include a co-ordinate (Eastings/Northings, Lat/Long or What3Words equivalent) or a property location identifier (UPRN, Address and Postcode)

**Timings**
*  The referral Sender **must** send the dispatch (or disposition) code identification time
*  The referral sender **should** send the callback time

**Scene Safety**
*  The referral Sender **must** send scene safety information in the referral
*  Where scene safety questions have not been asked, the scene safety flag **must** be populated with 'UNK' unknown.

**Flags**
NOT SURE IF WE NEED THIS

**Contacts** 
* A minimum of one contact (patient or third party) with a contact method (phone, email, etc.) of phone **must** be provided in requests
* All contacts **must** have a rank
* There **must** be only one contact with a rank of 1
* All contacts **must** have at least one contact method (phone, email, etc.)
* All contact methods **must** have a rank
* There **must** be only one contact method with a rank of 1
* The contact ranked 1 and the contact method ranked 1 **must** be the primary callback for the request
<br>
<br>
### Audit
* Sufficient information around any activity through the API and subsequent BaRS workflow **must** be persisted to aid support incidents and audit requirements
<br>
<br>
### Error Handling 
* Suppliers **must** adhere to the {{pagelink:Home/Design/BaRS-Core/Error-Handling.page.md, text:error handling guidance}} 
<br>
<br>
### Non Functional 
* Suppliers **must** adhere to the {{pagelink:Home/Design/BaRS-Core/Non-functional-requirements.page.md, text:non functional requirements}}
<br>
<br>
<hr>