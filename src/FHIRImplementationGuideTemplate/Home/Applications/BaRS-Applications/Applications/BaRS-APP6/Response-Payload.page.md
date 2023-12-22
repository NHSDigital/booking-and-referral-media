---
topic: APP6-ResponsePayload
---

## {{page-title}}

## Referral Response Payload (Status update)
This section provides guidance on the use of key resources, for the Receiver to create an Referral Response (Status update) to return to the Sender. See [ServiceRequest - Response](https://simplifier.net/nhsbookingandreferrals/bars-messagedefinition-servicerequest-response-referral-short) message definition for details of resources required for this payload.

_Note that Receivers will also have to build the capability to receive and process the Referral Request and Cancellation payloads_
<br>

### MessageHeader Resource
For detailed information on the use of MessageHeader please refer to the {{pagelink:core-SPMessageHeader, text:Standard Pattern - Message Header}}. 

The MessageHeader resource in the Referral Response should have the following resource elements set as follows:
* **MessageHeader.eventCoding** - **must** be populated with 'servicerequest-response'
* **MessageHeader.reasonCode** - **must** be 'new'
* **MessageHeader.focus** - **must** reference the Responder's current Encounter FHIR resource
* **MessageHeader.definition** - **must** adhere to [Referral Response](https://simplifier.net/NHSBookingandReferrals/BARS-MessageDefinition-ServiceRequest-Response-Referral-Short/~json) Message definition
* **MessgeHeader.Response** - **must** be the original request BundleID

### ServiceRequest Resource
The *ServiceRequest* is an echo of that sent by the Requester, and maintains the active state of the referral. The *ServiceRequest.status* at this point would stay as 'active'.

### Encounter Resource
The Responder's current *Encounter* is the focus resource in the Referral Response. This was originally the 'planned' Encounter created by the Receiver in the synchronous response to the Referral Request. 

This *Encounter* is used to represent the interaction between the patient and the Receiver healthcare service provider. 

When sending an Referral Response the Receiver **must**:
* Include the Receiver's current *Encounter* as the focus resource of the Referral Response
* Include the current *encounter.status* on the Receiver's current *Encounter*. This is to indicate to the Sender the progress of the case.
* *encounter.reasonCode* to be included on the Receiver's current *Encounter* to indicate that it is a response message.