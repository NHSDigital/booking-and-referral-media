---
topic: APP6-HowDoesItWork
---

## {{page-title}}

# {{page-title}}


This section describes how the primary operations used in this application work. The following  diagrams illustrate the workflows and interactions of the following use cases :
* CAD to CAD Out of Area referral
* CAD to CAD Call Assist Request
* CAD to CAD Mutual Aid Request

<br>

???? ADD WORKFLOW IMAGES AND REPLACE TEXT


This details a BaRS CAD to CAD Referral:

Actors:

| Use Case             | Referral Sender     | Referral Recipient |
| -------------------- | ------------------- | ------------------ |
| Out of Area referral | Call Receiving AST  | Home AST           |
| Call Assist Request  | Home AST            | Supporting AST     |
| Mutual Aid Request   | Home AST            | Supporting AST     |

Out of area calls

Calls may be re-routed by the BT Emergency Call Service to an Ambulance Service Trust (AST) outside of the geographic area of the incident (the Call Receiving AST) for the following reasons:
* The BT Intelligent Routing Platform (IRP) re-routes the call if the AST in the geographic area of the incident (the Home AST) does not have sufficient Call Handlers to answer the call within a given time frame
    * The Home AST has a 'buddying' arrangement with an out-of-area AST to take their calls under defined circumstances (e.g. system downtime, periods of surge)
    * A third party caller calls about a patient in another area
    * Calls where the incident is on the boundary between two ASTs
    
Call Assist Requests
- A Home AST may request support from a Supporting AST when they cannot send a resource to an incident within their geographic boundary of responsibility.
- The supporting AST may accept or reject this request
- If the Supporting AST rejects the request, the Home AST will make alternative arrangements
- If the Supporting AST accepts the request:
    - the Supporting AST is responsible for dispatching an appropriate resource within the time frame specified by the ARP Priority code
    - The Home AST may close the case on their CAD
    
Mutual Aid Requests

- A Home AST may request support from a Supporting AST when they cannot meet all of the resource requirements for and incident within their geographic boundary of responsibility.
- The supporting AST may accept or reject this request
- If the Supporting AST rejects the request, the Home AST will make alternative arrangements
- If the Supporting AST accepts the request:
    - the Supporting AST is responsible for dispatching the requested resource within the time frame specified in the request
    - The Home AST remains responsible for the case and for dispatching the resources not specified in the request
Note: The BaRS Referral may be used to support single patient Mutual aid requests. IT is not intended to replace processes relating to Mutual Aid Requests to support Major Incidents with multiple patients.

Receive Call
- When a call is re-routed by BT Emergency Services, call details are also sent electronically to the Referral Sender's AST's CAD via the Enhanced Information Service for Emergency Calls (EISEC) interface.
- For the Call Assist and Mutual aid use cases, the initial call may be received via BT Emergency Services EISEC interface or directly into the CAD e.g. Healthcare Professional (HCP) direct line

Create Case
- On receipt of this information the Call Receiving AST CAD creates a case that is subsequently further populated by system end users, the associated telephony system and other interfaced systems e.g. Clinical Decision Support Systems (CDSS) such as NHS Pathways and Advanced Medical Priority Dispatch System (AMPDS).

Pre Triage Sieve (PTS)
- On answering the call the Referral Sender AST will undertake a Pre Triage Sieve (PTS) to facilitate the early identification of patients with a potentially life-threatening emergency, in order that immediate dispatch of an appropriate resource can take place at the earliest possible point in the call cycle.
    - If a life-threatening emergency is identified by the PTS the Referral Sender AST may make a BaRS referral at this point in the call cycle, and all subsequent information will be communicated in BaRS Referral updates (see Sending a BaRS Referral)

Reason for Call
- The Referral Sender AST will capture a Reason for Call based on what the patient or their representative tells them. This may also be known as 'What's the Problem text or the Presenting complaint.

Nature of Call (NOC)
- The Referral Sender will capture a NOC code to facilitate the early identification of patients with a potentially life-threatening emergency.
    - If a life-threatening emergency is identified by the NOC, the Referral Sender AST may make a BaRS referral at this point in the call cycle, and all subsequent information will be communicated in BaRS Referral updates (see Sending a BaRS Referral)
    
Confirm Location
- The Referral Sender AST will record the location of the incident and confirm using Gazetteer services. This is undertaken at the earliest opportunity and may be prior or subsequent to PTS and NOC.

Record demographics
- The Referral Sender AST will capture the patient's baseline demographics where possible. This may be followed up by a Personal Demographics Service (PDS) search later in the call cycle.

Complete Triage
- The Referral Sender AST will complete a triage of the patient to determine the acuity of the case. This will typically be undertaken by a call handler on the Computer Aided Dispatch (CAD) system, using an approved Clinical Decision Support System (CDSS) such as NHS Pathways or AMPDS.

Sending a BaRS Referral
- The Referral Receiver is identified based on nationally agreed polygons that set geographic boundaries of responsibility for each AST. Service discovery will use these polygons to ascertain the ServiceID of the Referral Receiver.
- The Service ID is used to query the BaRS Endpoint Catalogue to identify the Referral Recipient's CAD system's endpoint details
- The Referral Sender AST will send the BaRS Referral to the Referral Recipient AST, which includes information required by the Referral Recipient AST to continue the patent's clinical care. This will also include the JourneyID created at the patient's first contact.

Create Case
- The Referral Recipient AST CAD will create a new case on receipt of the BaRS Referral and populate it with the details from the Referral Sender AST

Acknowledge Receipt

- The Referral Recipient AST CAD will send an acknowledgment back to the Referral Sender AST, when it has successfully processed the payload. If it fails to do this it will send a BaRS error code.

Continue updates
- If additional or changed information about the case is captured by the Referral Sender AST, subsequent to sending the BaRS Referral, they may send a BaRS Referral Update to ensure that the Referral Recipient AST has the most up to date information.
- If the Sending AST no longer requires the Receiving AST to perform the validation, for example the patient calls back and says they do not require an ambulance, they may send a Cancellation.
- On receipt of a Referral Update, the Receiving AST will send an acknowledgment back to the Sending AST on when it has successfully processed the payload. If it fails to do this it will send a BaRS error code.

Manage Stack
- The Receiving AST will manage the case in accordance with the Ambulance Response Programme (ARP) Priority Level. This may include:
    - Dispatching an appropriate resource within the specified time frame
    - Validating the triage outcome
    - Referring onward to another care setting e.g. Emergency Department
- when the status of a case changes in the Receiving AST, a BaRS Status Update will be sent to the Sending AST so they are aware of the current case status.


- Prior to the CAS consultation the case will typically be posted to a queue on the CAS system for prioritisation, based on the validation breach time in the referral. This is determined locally or nationally from the triage outcome codes.
- The CAS Clinician will contact the patient, or their representative, utilising contact details in the referral message.
- On commencement of the consultation the CAS system sends an Interim Validation Response back to the Sending 999 AST to inform them that the validation activity is in progress.
- The CAS clinician undertakes a consultation to validate the Sending Service's triage outcome. The consultation will be informed by the clinical information sent by the requesting service. The outcome of the validation will be recorded in the CAS system.
- The outcome of the consultation under taken by the CAS clinician to validate the original 999 AST triage outcome, is sent to the Sending service in a Final Validation Response. This may include:
	* An outcome that requires an upgraded ambulance response from the Sending 999 AST
	* An outcome that requires an downgraded ambulance response from the Sending 999 AST
	* An outcome that requires an unchanged ambulance response from the Sending 999 AST
	* An outcome that can be met by the provision of care advice with or without an electronic prescription (Hear and Treat)
	* An outcome that can be met by the onward referral to another service provider e.g. ED
- On receipt of the Final Validation Response the 999 AST will update the case on the CAD and undertake the required action. This may include:
	* Moving the case from the pending stack to the dispatch stack and dispatching a resource within the timescales appropriate for the ARP Priority in the Final Validation Response.
	* Closing the case if an ambulance is not required. 

<br>
<br>

To support the workflows for this application of the standard the operations that need to be supported are:

<hr>

## Make a Referral
??? LEIGH I COPIED PSEUDO CODE FROM APP3 - PLEASE CHECK AND UPDATE

Making a referral for this application follows the {{pagelink:Core-StandardPattern, text:standard pattern for BaRS operations}}.

The message definition that defines this payload for this application is: {{link:MessageDefinition-BARS-MessageDefinition-ServiceRequest-Request-Referral}}
<p>

In addition to that the specific workflow parameters that are required are as follows:

<div class="nhsd-m-emphasis-box">
    <div class="nhsd-a-box nhsd-a-box--border-grey">
        <div class="nhsd-m-emphasis-box__content-box">
            <table>
                <thead>
                    <tr>
                        <th>Interaction</th>
                        <th>Method</th>
                        <th>Payload Focus  </th>
                        <th>Status Required (MessageHeader, ServiceRequest, Encounter)</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td rowspan=6>Referral Request (New)</td>
                        <td rowspan=6>POST /$process-message{servicerequest-request}</td>
                        <td rowspan=6>ServiceRequest (active)</td>
                        <td>MessageHeader (EventCoding) = servicerequest-request</td>
                    </tr>
                    <tr>
                        <td>MessageHeader (ReasonCode) = new</td>
                    </tr>
                    <tr>
                        <td>ServiceRequest (Status) = active</td>
                    </tr>
                    <tr>
                        <td>ServiceRequest (Category) = referral</td>
                    </tr>
                    <tr>
                        <td>Encounter (Status) = triaged/finished</td>
                    </tr>
                    <tr>
                        <td><b>All resources to include 'lastUpdated' value, under meta section</b></td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</div>

<p>

Additionally the HTTP request header would be:

```
NHSD-Target-Identifier = {Receiver Service Identifier}
X-Request-Id = <GUID_000001>
X-Correlation-Id = <GUID_000002>
NHSD-End-User-Organisation = {FHIR Organisation (Base64 Encoded)}
NHSD-Requesting-Practitioner = {FHIR Practitioner (Base64 Encoded)} 
NHSD-Requesting-Software =  {FHIR Device (Base64 Encoded)}
```

The HTTP response header would be:

```
X-Request-Id = <GUID_000001>
X-Correlation-Id = <GUID_000002>
```

### Cancel a Referral

To cancel a referral this application follows the {{pagelink:Core-StandardPattern, text:standard pattern for BaRS operations}} with an additional step. Before beginning the standard pattern as descbribed on the linked section, the referral **sender** must perform a read of the referral to be cancelled, from the referral **receiver**, prior to cancellation to ensure they are working with the most up-to date information and it has not already been actioned. This is done by performing a "GET ServiceRequest by ID" call to the **receiving** system's corresponding API endpoint (via the BaRS proxy).

The response to this request will be the requested ServiceRequest resource which should be checked for its current status to ensure it does not already have a status of "revoked" or "completed". If not, this version of the ServiceRequest should be used when re-submitting the modified resource in the POST bundle as described in the {{pagelink:core-standardpattern, text:standard pattern}}.

The message definition that defines this payload for this application is: {{link:messagedefinition-barsmessagedefinitionservicerequestrequestcancelled}}

As a general princple, when performing an update type of operation (of which cancellation is a special case), only the focus resource, any resources that are mandated due to contextual, linking or referential integrity reasons and any resources that include elements that are being changed, **should** be include. This is always defined within the relevent message definition.

If the update-to-cancel is taking place as part of a re-referral routine, once the cancellation is complete, the new referral message can be sent. This step in the workflow would follow the same process as 'Make a referral' detailed above.

In addition the specific workflow parameters that are required are as follows:

<div class="nhsd-m-emphasis-box">
    <div class="nhsd-a-box nhsd-a-box--border-grey">
        <div class="nhsd-m-emphasis-box__content-box">
            <table>
                <thead>
                    <tr>
                        <th>Interaction</th>
                        <th>Method</th>
                        <th>Payload Focus  </th>
                        <th>Status Required (MessageHeader, ServiceRequest, Encounter)</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>Get Referral</td>
                        <td>GET /ServiceRequest{id}</td>
                        <td>n/a</td>
                        <td>n/a</td>
                    </tr>
                    <tr>
                        <td rowspan=8>Referral Request (Cancel)</td>
                        <td rowspan=8>POST /$process-message{servicerequest-request}</td>
                        <td rowspan=8>ServiceRequest (revoked)</td>
                        <td>MessageHeader (EventCoding) = servicerequest-request</td>
                    </tr>
                    <tr>
                        <td>MessageHeader (ReasonCode) = update</td>
                    </tr>
                    <tr>
                        <td>ServiceRequest (Status) = revoked</td>
                    </tr>
                    <tr>
                        <td>ServiceRequest (Category) = referral</td>
                    </tr>
                    <tr>
                        <td>Encounter (Status) = triaged/finished</td>
                    </tr>
                    <tr rowspan=3>
                        <td>
                            <b>All resources to include 'lastUpdated' value, under the meta section,</b>                    
                            <b>which must be a later timestamp, on updates, if the content of a particular resource contains updated info. Otherwise,</b>
                            <b>maintain the timestamp originally sent.</b>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</div>

<p>

Additionally the HTTP request header for the **GET ServiceRequest** would be:

```
NHSD-Target-Identifier = {Receiver Service Identifier}
X-Request-Id = <GUID_107>
X-Correlation-Id = <GUID_108>
NHSD-End-User-Organisation = {FHIR Organisation (Base64 Encoded)}
NHSD-Requesting-Practitioner = {FHIR Practitioner (Base64 Encoded)} 
NHSD-Requesting-Software =  {FHIR Device (Base64 Encoded)}
```

The HTTP response header for the **GET ServiceRequest** would be:

```
X-Request-Id = <GUID_107>
X-Correlation-Id = <GUID_108>
```

the HTTP request header for the **POST $process-message** would be:

```
NHSD-Target-Identifier = {Receiver Service Identifier}
X-Request-Id = <GUID_000003>
X-Correlation-Id = <GUID_000002>
NHSD-End-User-Organisation = {FHIR Organisation (Base64 Encoded)}
NHSD-Requesting-Practitioner = {FHIR Practitioner (Base64 Encoded)} 
NHSD-Requesting-Software =  {FHIR Device (Base64 Encoded)}
```

The HTTP response header for the **POST $process-message** would be:

```
X-Request-Id = <GUID_000003>
X-Correlation-Id = <GUID_000002>
```

### Bundle Processing - detailed

Below is a pseudo code example of how a bundle could be processed based on the above workflow variables:

<details>
    <summary>> <b class="barslink">Logical - Based on a logical step through in a code format</b></summary>

```c#
Receive_Request
{
	initialise_variable "messageType" 
	initialise_variable "MessageReason" 
	initialise_variable "RequestType"
	
	//HTTP_Headers
	{
		if (HttpHeaders is null || HttpHeaders not Guid )
			OperationOutcome.issue.code = "invalid"
			throw exception with "REC_BAD_REQUEST"
			then return with HTTP.ResponseCode 400
		else if (HttpHeaders.RequestId == RequestId.AlreadyReceived)
			OperationOutcome.issue.code = "duplicate"
			throw exception with "REC_CONFLICT"
			then return with HTTP.ResponseCode 409
	}
	//Bundle
	{
		if(Bundle.meta.versionID is null)
			OperationOutcome.issue.code = "invariant"
			throw exception with "REC_BAD_REQUEST"
			then return with HTTP.ResponseCode 422
		else if!(Bundle.meta.versionID in versionID.supported)
			OperationOutcome.issue.code = "not-supported"
			throw exception with "REC_UNPROCESSABLE_ENTITY"
			then return with HTTP.ResponseCode 422
	}
	//Contents;
	{
		switch(MessageHeader.eventCoding)
		{
			case "servicerequest-request":
				if (MessageHeader.reason.code == "new" && ServiceRequest.status == "active")
					{
						switch(ServiceRequest.Category)
						{
							case "Referral":
								if (Careplan.status != "completed")
								{
									RequestType = "unknown"
									OperationOutcome.issue.code = "invariant"//A content validation rule failed
									throw exception with "REC_BAD_REQUEST"
									then return  HTTP.ResponseCode 400
								}
								else if(Encounter.Status.In("triaged","finished"))
									RequestType = "Im Receiving a new Referral"
								else
									RequestType = "unknown"
									OperationOutcome.issue.code = "invariant"//A content validation rule failed
									throw exception with "REC_BAD_REQUEST"
									then return  HTTP.ResponseCode 400
								break;
							default:
								RequestType = "unknown"
								OperationOutcome.issue.code = "invariant"//A content validation rule failed
								throw exception with "REC_BAD_REQUEST"
								then return  HTTP.ResponseCode 400;
						}
					}
				else if (MessageHeader.reason.code == "update")
					{
						switch(ServiceRequest.category)
						{
							case "Referral":
								if(ServiceRequest.status.In("entered-in-error","revoked"))
								{RequestType = "im receiving a cancelled referral"}
								else
								{
									RequestType = "unknown"
									OperationOutcome.issue.code = "invariant"//A content validation rule failed
									throw exception with "REC_BAD_REQUEST"
									then return  HTTP.ResponseCode 400								
								}
								break;
							default:
								RequestType = "unknown"
								OperationOutcome.issue.code = "invariant"//A content validation rule failed
								throw exception with "REC_BAD_REQUEST"
								then return  HTTP.ResponseCode 400;
						}
					}
				else
				{
					RequestType = "unknown"
					OperationOutcome.issue.code = "invariant"//A content validation rule failed
					throw exception with "REC_BAD_REQUEST"
					then return  HTTP.ResponseCode 400}
				break;
			case "servicerequest-response":
				if (MessageHeader.Response is null )
				{
						RequestType = "Invalid servicerequest-response"
						OperationOutcome.issue.code = "invariant"//A content validation rule failed
						throw exception with "REC_BAD_REQUEST"
						then return  HTTP.ResponseCode 400;
				}
				else if ( !Message.Response.identifier.existsLocally())
				{
						RequestType = "none or invalid response ID"
						OperationOutcome.issue.code = "not-found"//A content validation rule failed
						throw exception with "REC_NOT_FOUND"
						then return  HTTP.ResponseCode 404;
				}
				switch (ServiceRequest.Category)
					{
						case "Referral":
							if (ServiceRequest.status == "revoked" && MessageHeader.reason.code == "new")
							{ RequestType = "im receiving a Safeguarding DNA response (noshow)" } 
							else
							{
								RequestType = "unknown"
								OperationOutcome.issue.code = "invariant"//A content validation rule failed
								throw exception with "REC_BAD_REQUEST"
								then return  HTTP.ResponseCode 400;
							}
							break;
						default:
							RequestType = "unknown"
							OperationOutcome.issue.code = "invariant"//A content validation rule failed
							throw exception with "REC_BAD_REQUEST"
							then return  HTTP.ResponseCode 400;
					}
		}
		
	}
    //Submit
	{
		
		if (Message == "update")
		{
			if (currentLocalData.LastUpdated > originaRequest.ReceivedDate)
			{
				OperationOutcome.issue.code = "conflict"
				throw exception with 'REC_CONFLICT'
				then return with HTTP.ResponseCode 409
				break;
			}		
			foreach (Entry in Bundle)
			{
				if (currentLocalData.Item.exists)
				{
					if (currentLocalData.LastUpdated > originaRequest.Received)
					{
						OperationOutcome.issue.code = "conflict"
						throw exception with 'REC_CONFLICT'
						then return with HTTP.ResponseCode 409
						break;
					}
					if(Entry.LastUpdated > currentLocalData.Item.meta.LastUpdated && Entry.fullUrl = currentLocalData.Item.fullUrl)
						currentLocalData.Item = Entry.Item
						Entry.SubmitWith(currentLocalData.Item.meta.LastUpdated == Entry.LastUpdated )
					else
						ignore
				}
				else
					Entry.SubmitWith(currentLocalData.Item.meta.LastUpdated == Entry.LastUpdated )					
			}
			Submit(currentLocalData.Bundle.meta.LastUpdated = Bundle.Meta.LastUpdated)
			return HTTP.ResponseCode 200 'OK'
		}
		else
			{
				foreach(Entry in Bundle)
				{
					Entry.SubmitWith(currentLocalData.Item.meta.LastUpdated == Entry.LastUpdated )
					Submit(currentLocalData.Bundle.meta.LastUpdated = Bundle.Meta.LastUpdated)
					return HTTP.ResponseCode 200 'OK'
				}
			}
	}	
}	


```

</details>
<br>

<hr>