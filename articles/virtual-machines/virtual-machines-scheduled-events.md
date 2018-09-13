---
title: Scheduled Events with Azure Metadata Service | Microsoft Docs
description: React to Impactful Events on your Virtual Machine before they happen.
services: virtual-machines-windows, virtual-machines-linux, cloud-services
documentationcenter: ''
author: zivraf
manager: timlt
editor: ''
tags: ''
ms.assetid: 28d8e1f2-8e61-4fbe-bfe8-80a68443baba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/10/2016
ms.author: zivr
ms.openlocfilehash: 18c7a013c01fee26c5455535af6d9fba2b98fac7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552645"
---
# <a name="azure-metadata-service---scheduled-events-preview"></a>Azure Metadata Service - Scheduled Events (Preview)

> [!NOTE] 
> Previews are made available to you on the condition that you agree to the terms of use. For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews.] (https://azure.microsoft.com/en-us/support/legal/preview-supplemental-terms/)
>

Scheduled Events is one of the subservices under Azure Metadata Service that surfaces information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption. It is available for all Azure Virtual Machine types including PaaS and IaaS. Scheduled Events gives your Virtual Machine time to perform preventive tasks and minimize the effect of an event. 


## <a name="introduction---why-scheduled-events"></a>Introduction - Why Scheduled Events?

With Scheduled Events, you can take steps to limit the impact on your service. Multi-instance workloads, which use replication techniques to maintain state, may be vulnerable to frequent outages happening across multiple instances. Such outages may result in expensive tasks (for example, rebuilding indexes) or even a replica loss. In many other cases, using graceful shutdown sequence improves the overall service availability. For example, completing (or canceling) in-flight transactions, reassigning other tasks to other VMs in the cluster (manual failover), remove the Virtual Machine from a load balancer pool. There are cases where notifying an administrator about upcoming event or even just logging such an event help improving the serviceability of applications hosted in the cloud.
Azure Metadata Service surfaces Scheduled Events in the following use cases:
-   Platform initiated maintenance (for example, Host OS rollout)
-   User initiated calls (for example, user restarts or redeploy a VM)


## <a name="scheduled-events---the-basics"></a>Scheduled Events - The Basics  

Azure Metadata service exposes information about running Virtual Machines using a REST Endpoint from within the VM. The information is available via a Non-routable IP so that it is not exposed outside the VM.

### <a name="scope"></a>Scope
Scheduled events are surfaced to all Virtual Machines in a cloud service or to all Virtual Machines in an Availability Set. As a result, you should check the **Resources** field in the event to identify which VMs are going to be impacted. 

### <a name="discover-the-endpoint"></a>Discover the Endpoint
In the case where a Virtual Machine is created within a Virtual Network (VNet), the metadata service is available from the non-routable IP of: 169.254.169.254 Otherwise, in the default cases for cloud services and classic VMs, an additional logic is required to discover the endpoint to use. Refer to this sample to learn how to [discover the host endpoint] (https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm)

### <a name="versioning"></a>Versioning 
The Metadata Service uses a versioned API in the following format: http://{ip}/metadata/{version}/scheduledevents It is recommended that your service consumes the latest version available at: http://{ip}/metadata/latest/scheduledevents

### <a name="using-headers"></a>Using Headers
When you query the Metadata Service, you must provide the following header *Metadata: true*. 

### <a name="enable-scheduled-events"></a>Enable Scheduled Events
The first time you call for scheduled events, Azure implicitly enables the feature on your Virtual Machine. As a result, you should expect a delayed response in your first call of up to two minutes.

### <a name="testing-your-logic-with-user-initiated-operations"></a>Testing your logic with user initiated operations
To test your logic, you can use the Azure portal, API, CLI, or PowerShell to initiate operations resulting in scheduled events. Restarting a virtual machine results in a scheduled event with an event type equal to Reboot. Redeploying a virtual machine results in a scheduled event with an event type equal to Redeploy.
In both cases, the user initiated operation takes longer to complete since scheduled events enable more time for an application to gracefully shut down. 

## <a name="using-the-api"></a>Using the API

### <a name="query-for-events"></a>Query for events
You can query for Scheduled Events simply by making the following call

    curl -H Metadata:true http://169.254.169.254/metadata/latest/scheduledevents

A response contains an array of scheduled events. An empty array means that there are currently no events scheduled.
In the case where there are scheduled events, the response contains an array of events: 

    {
     "DocumentIncarnation":{IncarnationID},
     "Events":[
          {
                "EventId":{eventID},
                "EventType":"Reboot" | "Redeploy" | "Freeze",
                "ResourceType":"VirtualMachine",
                "Resources":[{resourceName}],
                "EventStatus":"Scheduled" | "Started",
                "NotBefore":{timeInUTC},              
         }
     ]
    }

EventType Captures the expected impact on the Virtual Machine where:
- Freeze: The Virtual Machine is scheduled to pause for few seconds. There is no impact on memory, open files, or network connections
- Reboot: The Virtual Machine is scheduled for reboot (memory is wiped).
- Redeploy: The Virtual Machine is scheduled to move to another node (ephemeral disk are lost). 

When an event is scheduled (Status = Scheduled), Azure shares the time after which the event can start (specified in the NotBefore field).

### <a name="starting-an-event-expedite"></a>Starting an event (expedite)

Once you have learned of an upcoming event and completed your logic for graceful shutdown, you can indicate Azure to move faster (when possible) by making a **POST** call 
 

## <a name="powershell-sample"></a>PowerShell Sample 

The following sample reads the metadata server for scheduled events and approves the events.

```PowerShell
# How to get scheduled events 
function GetScheduledEvents($uri)
{
    $scheduledEvents = Invoke-RestMethod -Headers @{"Metadata"="true"} -URI $uri -Method get
    $json = ConvertTo-Json $scheduledEvents
    Write-Host "Received following events: `n" $json
    return $scheduledEvents
}

# How to approve a scheduled event
function ApproveScheduledEvent($eventId, $uri)
{    
    # Create the Scheduled Events Approval Json
    $startRequests = [array]@{"EventId" = $eventId}
    $scheduledEventsApproval = @{"StartRequests" = $startRequests} 
    $approvalString = ConvertTo-Json $scheduledEventsApproval

    Write-Host "Approving with the following: `n" $approvalString

    # Post approval string to scheduled events endpoint
    Invoke-RestMethod -Uri $uri -Headers @{"Metadata"="true"} -Method POST -Body $approvalString
}

# Add logic relevant to your service here
function HandleScheduledEvents($scheduledEvents)
{

}

######### Sample Scheduled Events Interaction #########

# Set up the scheduled events uri for VNET enabled VM
$localHostIP = "169.254.169.254"
$scheduledEventURI = 'http://{0}/metadata/latest/scheduledevents' -f $localHostIP 


# Get the document
$scheduledEvents = GetScheduledEvents $scheduledEventURI


# Handle events however is best for your service
HandleScheduledEvents $scheduledEvents


# Approve events when ready (optional)
foreach($event in $scheduledEvents.Events)
{
    Write-Host "Current Event: `n" $event
    $entry = Read-Host "`nApprove event? Y/N"
    if($entry -eq "Y" -or $entry -eq "y")
    {
    ApproveScheduledEvent $event.EventId $scheduledEventURI 
    }
}
``` 


## <a name="c-sample"></a>C\# Sample 
The following sample is of a client surfacing APIs to communicate with the Metadata Service
```csharp
   public class ScheduledEventsClient
    {
        private readonly string scheduledEventsEndpoint;
        private readonly string defaultIpAddress = "169.254.169.254"; 

        public ScheduledEventsClient()
        {
            scheduledEventsEndpoint = string.Format("http://{0}/metadata/latest/scheduledevents", defaultIpAddress);
        }
        /// Retrieve Scheduled Events 
        public string GetDocument()
        {
            Uri cloudControlUri = new Uri(scheduledEventsEndpoint);
            using (var webClient = new WebClient())
            {
                webClient.Headers.Add("Metadata", "true");
                return webClient.DownloadString(cloudControlUri);
            }   
        }

        /// Issues a post request to the scheduled events endpoint with the given json string
        public void PostResponse(string jsonPost)
        {
            using (var webClient = new WebClient())
            {
                webClient.Headers.Add("Content-Type", "application/json");
                webClient.UploadString(scheduledEventsEndpoint, jsonPost);
            }
        }
    }

```
Scheduled Events could be parsed using the following data structures 

```csharp
    public class ScheduledEventsDocument
    {
        public List<CloudControlEvent> Events { get; set; }
    }

    public class CloudControlEvent
    {
        public string EventId { get; set; }
        public string EventStatus { get; set; }
        public string EventType { get; set; }
        public string ResourceType { get; set; }
        public List<string> Resources { get; set; }
        public DateTime NoteBefore { get; set; }
    }

    public class ScheduledEventsApproval
    {
        public List<StartRequest> StartRequests = new List<StartRequest>();
    }

    public class StartRequest
    {
        [JsonProperty("EventId")]
        private string eventId;

        public StartRequest(string eventId)
        {
            this.eventId = eventId;
        }
    }

```

A Sample Program using the client to retrieve, handle, and acknowledge events:   

```csharp
public class Program
    {
    static ScheduledEventsClient client;
    static void Main(string[] args)
    {
        while (true)
        {
            client = new ScheduledEventsClient();
            string json = client.GetDocument();
            ScheduledEventsDocument scheduledEventsDocument = JsonConvert.DeserializeObject<ScheduledEventsDocument>(json);

            HandleEvents(scheduledEventsDocument.Events);

            // Wait for user response
            Console.WriteLine("Press Enter to approve executing events\n");
            Console.ReadLine();

            // Approve events
            ScheduledEventsApproval scheduledEventsApprovalDocument = new ScheduledEventsApproval();
            foreach (CloudControlEvent ccevent in scheduledEventsDocument.Events)
            {
                scheduledEventsApprovalDocument.StartRequests.Add(new StartRequest(ccevent.EventId));
            }
            if (scheduledEventsApprovalDocument.StartRequests.Count > 0)
            {
                // Serialize using Newtonsoft.Json
                string approveEventsJsonDocument =
                    JsonConvert.SerializeObject(scheduledEventsApprovalDocument);

                Console.WriteLine($"Approving events with json: {approveEventsJsonDocument}\n");
                client.PostResponse(approveEventsJsonDocument);
            }

            Console.WriteLine("Complete. Press enter to repeat\n\n");
            Console.ReadLine();
            Console.Clear();
        }
    }

    private static void HandleEvents(List<CloudControlEvent> events)
    {
        // Add logic for handling events here
    }
}

```

## <a name="python-sample"></a>Python Sample 

```python


#!/usr/bin/python

import json
import urllib2
import socket
import sys

metadata_url="http://169.254.169.254/metadata/latest/scheduledevents"
headers="{Metadata:true}"
this_host=socket.gethostname()

def get_scheduled_events():
   req=urllib2.Request(metadata_url)
   req.add_header('Metadata','true')
   resp=urllib2.urlopen(req)
   data=json.loads(resp.read())
   return data

def handle_scheduled_events(data):
    for evt in data['Events']:
        eventid=evt['EventId']
        status=evt['EventStatus']
        resources=evt['Resources'][0]
        eventype=evt['EventType']
        restype=evt['ResourceType']
        notbefore=evt['NotBefore'].replace(" ","_")
        if this_host in evt['Resources'][0]:
            print "+ Scheduled Event. This host is scheduled for " + eventype + " not before " + notbefore
            print "++ Add you logic here"

def main():
   data=get_scheduled_events()
   handle_scheduled_events(data)
   

if __name__ == '__main__':
  main()
  sys.exit(0)


```
## <a name="next-steps"></a>Next Steps 
[Planned maintenance for virtual machines in Azure](linux/planned-maintenance.md)
