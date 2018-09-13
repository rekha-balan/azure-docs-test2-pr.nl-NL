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
# <a name="azure-metadata-service---scheduled-events-preview"></a><span data-ttu-id="061aa-103">Azure Metadata Service - Scheduled Events (Preview)</span><span class="sxs-lookup"><span data-stu-id="061aa-103">Azure Metadata Service - Scheduled Events (Preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="061aa-104">Previews are made available to you on the condition that you agree to the terms of use.</span><span class="sxs-lookup"><span data-stu-id="061aa-104">Previews are made available to you on the condition that you agree to the terms of use.</span></span> <span data-ttu-id="061aa-105">For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews.] (https://azure.microsoft.com/en-us/support/legal/preview-supplemental-terms/)</span><span class="sxs-lookup"><span data-stu-id="061aa-105">For more information, see [Microsoft Azure Supplemental Terms of Use for Microsoft Azure Previews.] (https://azure.microsoft.com/en-us/support/legal/preview-supplemental-terms/)</span></span>
>

<span data-ttu-id="061aa-106">Scheduled Events is one of the subservices under Azure Metadata Service that surfaces information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span><span class="sxs-lookup"><span data-stu-id="061aa-106">Scheduled Events is one of the subservices under Azure Metadata Service that surfaces information regarding upcoming events (for example, reboot) so your application can prepare for them and limit disruption.</span></span> <span data-ttu-id="061aa-107">It is available for all Azure Virtual Machine types including PaaS and IaaS.</span><span class="sxs-lookup"><span data-stu-id="061aa-107">It is available for all Azure Virtual Machine types including PaaS and IaaS.</span></span> <span data-ttu-id="061aa-108">Scheduled Events gives your Virtual Machine time to perform preventive tasks and minimize the effect of an event.</span><span class="sxs-lookup"><span data-stu-id="061aa-108">Scheduled Events gives your Virtual Machine time to perform preventive tasks and minimize the effect of an event.</span></span> 


## <a name="introduction---why-scheduled-events"></a><span data-ttu-id="061aa-109">Introduction - Why Scheduled Events?</span><span class="sxs-lookup"><span data-stu-id="061aa-109">Introduction - Why Scheduled Events?</span></span>

<span data-ttu-id="061aa-110">With Scheduled Events, you can take steps to limit the impact on your service.</span><span class="sxs-lookup"><span data-stu-id="061aa-110">With Scheduled Events, you can take steps to limit the impact on your service.</span></span> <span data-ttu-id="061aa-111">Multi-instance workloads, which use replication techniques to maintain state, may be vulnerable to frequent outages happening across multiple instances.</span><span class="sxs-lookup"><span data-stu-id="061aa-111">Multi-instance workloads, which use replication techniques to maintain state, may be vulnerable to frequent outages happening across multiple instances.</span></span> <span data-ttu-id="061aa-112">Such outages may result in expensive tasks (for example, rebuilding indexes) or even a replica loss.</span><span class="sxs-lookup"><span data-stu-id="061aa-112">Such outages may result in expensive tasks (for example, rebuilding indexes) or even a replica loss.</span></span> <span data-ttu-id="061aa-113">In many other cases, using graceful shutdown sequence improves the overall service availability.</span><span class="sxs-lookup"><span data-stu-id="061aa-113">In many other cases, using graceful shutdown sequence improves the overall service availability.</span></span> <span data-ttu-id="061aa-114">For example, completing (or canceling) in-flight transactions, reassigning other tasks to other VMs in the cluster (manual failover), remove the Virtual Machine from a load balancer pool.</span><span class="sxs-lookup"><span data-stu-id="061aa-114">For example, completing (or canceling) in-flight transactions, reassigning other tasks to other VMs in the cluster (manual failover), remove the Virtual Machine from a load balancer pool.</span></span> <span data-ttu-id="061aa-115">There are cases where notifying an administrator about upcoming event or even just logging such an event help improving the serviceability of applications hosted in the cloud.</span><span class="sxs-lookup"><span data-stu-id="061aa-115">There are cases where notifying an administrator about upcoming event or even just logging such an event help improving the serviceability of applications hosted in the cloud.</span></span>
<span data-ttu-id="061aa-116">Azure Metadata Service surfaces Scheduled Events in the following use cases:</span><span class="sxs-lookup"><span data-stu-id="061aa-116">Azure Metadata Service surfaces Scheduled Events in the following use cases:</span></span>
-   <span data-ttu-id="061aa-117">Platform initiated maintenance (for example, Host OS rollout)</span><span class="sxs-lookup"><span data-stu-id="061aa-117">Platform initiated maintenance (for example, Host OS rollout)</span></span>
-   <span data-ttu-id="061aa-118">User initiated calls (for example, user restarts or redeploy a VM)</span><span class="sxs-lookup"><span data-stu-id="061aa-118">User initiated calls (for example, user restarts or redeploy a VM)</span></span>


## <a name="scheduled-events---the-basics"></a><span data-ttu-id="061aa-119">Scheduled Events - The Basics</span><span class="sxs-lookup"><span data-stu-id="061aa-119">Scheduled Events - The Basics</span></span>  

<span data-ttu-id="061aa-120">Azure Metadata service exposes information about running Virtual Machines using a REST Endpoint from within the VM.</span><span class="sxs-lookup"><span data-stu-id="061aa-120">Azure Metadata service exposes information about running Virtual Machines using a REST Endpoint from within the VM.</span></span> <span data-ttu-id="061aa-121">The information is available via a Non-routable IP so that it is not exposed outside the VM.</span><span class="sxs-lookup"><span data-stu-id="061aa-121">The information is available via a Non-routable IP so that it is not exposed outside the VM.</span></span>

### <a name="scope"></a><span data-ttu-id="061aa-122">Scope</span><span class="sxs-lookup"><span data-stu-id="061aa-122">Scope</span></span>
<span data-ttu-id="061aa-123">Scheduled events are surfaced to all Virtual Machines in a cloud service or to all Virtual Machines in an Availability Set.</span><span class="sxs-lookup"><span data-stu-id="061aa-123">Scheduled events are surfaced to all Virtual Machines in a cloud service or to all Virtual Machines in an Availability Set.</span></span> <span data-ttu-id="061aa-124">As a result, you should check the **Resources** field in the event to identify which VMs are going to be impacted.</span><span class="sxs-lookup"><span data-stu-id="061aa-124">As a result, you should check the **Resources** field in the event to identify which VMs are going to be impacted.</span></span> 

### <a name="discover-the-endpoint"></a><span data-ttu-id="061aa-125">Discover the Endpoint</span><span class="sxs-lookup"><span data-stu-id="061aa-125">Discover the Endpoint</span></span>
<span data-ttu-id="061aa-126">In the case where a Virtual Machine is created within a Virtual Network (VNet), the metadata service is available from the non-routable IP of: 169.254.169.254 Otherwise, in the default cases for cloud services and classic VMs, an additional logic is required to discover the endpoint to use.</span><span class="sxs-lookup"><span data-stu-id="061aa-126">In the case where a Virtual Machine is created within a Virtual Network (VNet), the metadata service is available from the non-routable IP of: 169.254.169.254 Otherwise, in the default cases for cloud services and classic VMs, an additional logic is required to discover the endpoint to use.</span></span> <span data-ttu-id="061aa-127">Refer to this sample to learn how to [discover the host endpoint] (https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm)</span><span class="sxs-lookup"><span data-stu-id="061aa-127">Refer to this sample to learn how to [discover the host endpoint] (https://github.com/azure-samples/virtual-machines-python-scheduled-events-discover-endpoint-for-non-vnet-vm)</span></span>

### <a name="versioning"></a><span data-ttu-id="061aa-128">Versioning</span><span class="sxs-lookup"><span data-stu-id="061aa-128">Versioning</span></span> 
<span data-ttu-id="061aa-129">The Metadata Service uses a versioned API in the following format: http://{ip}/metadata/{version}/scheduledevents It is recommended that your service consumes the latest version available at: http://{ip}/metadata/latest/scheduledevents</span><span class="sxs-lookup"><span data-stu-id="061aa-129">The Metadata Service uses a versioned API in the following format: http://{ip}/metadata/{version}/scheduledevents It is recommended that your service consumes the latest version available at: http://{ip}/metadata/latest/scheduledevents</span></span>

### <a name="using-headers"></a><span data-ttu-id="061aa-130">Using Headers</span><span class="sxs-lookup"><span data-stu-id="061aa-130">Using Headers</span></span>
<span data-ttu-id="061aa-131">When you query the Metadata Service, you must provide the following header *Metadata: true*.</span><span class="sxs-lookup"><span data-stu-id="061aa-131">When you query the Metadata Service, you must provide the following header *Metadata: true*.</span></span> 

### <a name="enable-scheduled-events"></a><span data-ttu-id="061aa-132">Enable Scheduled Events</span><span class="sxs-lookup"><span data-stu-id="061aa-132">Enable Scheduled Events</span></span>
<span data-ttu-id="061aa-133">The first time you call for scheduled events, Azure implicitly enables the feature on your Virtual Machine.</span><span class="sxs-lookup"><span data-stu-id="061aa-133">The first time you call for scheduled events, Azure implicitly enables the feature on your Virtual Machine.</span></span> <span data-ttu-id="061aa-134">As a result, you should expect a delayed response in your first call of up to two minutes.</span><span class="sxs-lookup"><span data-stu-id="061aa-134">As a result, you should expect a delayed response in your first call of up to two minutes.</span></span>

### <a name="testing-your-logic-with-user-initiated-operations"></a><span data-ttu-id="061aa-135">Testing your logic with user initiated operations</span><span class="sxs-lookup"><span data-stu-id="061aa-135">Testing your logic with user initiated operations</span></span>
<span data-ttu-id="061aa-136">To test your logic, you can use the Azure portal, API, CLI, or PowerShell to initiate operations resulting in scheduled events.</span><span class="sxs-lookup"><span data-stu-id="061aa-136">To test your logic, you can use the Azure portal, API, CLI, or PowerShell to initiate operations resulting in scheduled events.</span></span> <span data-ttu-id="061aa-137">Restarting a virtual machine results in a scheduled event with an event type equal to Reboot.</span><span class="sxs-lookup"><span data-stu-id="061aa-137">Restarting a virtual machine results in a scheduled event with an event type equal to Reboot.</span></span> <span data-ttu-id="061aa-138">Redeploying a virtual machine results in a scheduled event with an event type equal to Redeploy.</span><span class="sxs-lookup"><span data-stu-id="061aa-138">Redeploying a virtual machine results in a scheduled event with an event type equal to Redeploy.</span></span>
<span data-ttu-id="061aa-139">In both cases, the user initiated operation takes longer to complete since scheduled events enable more time for an application to gracefully shut down.</span><span class="sxs-lookup"><span data-stu-id="061aa-139">In both cases, the user initiated operation takes longer to complete since scheduled events enable more time for an application to gracefully shut down.</span></span> 

## <a name="using-the-api"></a><span data-ttu-id="061aa-140">Using the API</span><span class="sxs-lookup"><span data-stu-id="061aa-140">Using the API</span></span>

### <a name="query-for-events"></a><span data-ttu-id="061aa-141">Query for events</span><span class="sxs-lookup"><span data-stu-id="061aa-141">Query for events</span></span>
<span data-ttu-id="061aa-142">You can query for Scheduled Events simply by making the following call</span><span class="sxs-lookup"><span data-stu-id="061aa-142">You can query for Scheduled Events simply by making the following call</span></span>

    curl -H Metadata:true http://169.254.169.254/metadata/latest/scheduledevents

<span data-ttu-id="061aa-143">A response contains an array of scheduled events.</span><span class="sxs-lookup"><span data-stu-id="061aa-143">A response contains an array of scheduled events.</span></span> <span data-ttu-id="061aa-144">An empty array means that there are currently no events scheduled.</span><span class="sxs-lookup"><span data-stu-id="061aa-144">An empty array means that there are currently no events scheduled.</span></span>
<span data-ttu-id="061aa-145">In the case where there are scheduled events, the response contains an array of events:</span><span class="sxs-lookup"><span data-stu-id="061aa-145">In the case where there are scheduled events, the response contains an array of events:</span></span> 

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

<span data-ttu-id="061aa-146">EventType Captures the expected impact on the Virtual Machine where:</span><span class="sxs-lookup"><span data-stu-id="061aa-146">EventType Captures the expected impact on the Virtual Machine where:</span></span>
- <span data-ttu-id="061aa-147">Freeze: The Virtual Machine is scheduled to pause for few seconds.</span><span class="sxs-lookup"><span data-stu-id="061aa-147">Freeze: The Virtual Machine is scheduled to pause for few seconds.</span></span> <span data-ttu-id="061aa-148">There is no impact on memory, open files, or network connections</span><span class="sxs-lookup"><span data-stu-id="061aa-148">There is no impact on memory, open files, or network connections</span></span>
- <span data-ttu-id="061aa-149">Reboot: The Virtual Machine is scheduled for reboot (memory is wiped).</span><span class="sxs-lookup"><span data-stu-id="061aa-149">Reboot: The Virtual Machine is scheduled for reboot (memory is wiped).</span></span>
- <span data-ttu-id="061aa-150">Redeploy: The Virtual Machine is scheduled to move to another node (ephemeral disk are lost).</span><span class="sxs-lookup"><span data-stu-id="061aa-150">Redeploy: The Virtual Machine is scheduled to move to another node (ephemeral disk are lost).</span></span> 

<span data-ttu-id="061aa-151">When an event is scheduled (Status = Scheduled), Azure shares the time after which the event can start (specified in the NotBefore field).</span><span class="sxs-lookup"><span data-stu-id="061aa-151">When an event is scheduled (Status = Scheduled), Azure shares the time after which the event can start (specified in the NotBefore field).</span></span>

### <a name="starting-an-event-expedite"></a><span data-ttu-id="061aa-152">Starting an event (expedite)</span><span class="sxs-lookup"><span data-stu-id="061aa-152">Starting an event (expedite)</span></span>

<span data-ttu-id="061aa-153">Once you have learned of an upcoming event and completed your logic for graceful shutdown, you can indicate Azure to move faster (when possible) by making a **POST** call</span><span class="sxs-lookup"><span data-stu-id="061aa-153">Once you have learned of an upcoming event and completed your logic for graceful shutdown, you can indicate Azure to move faster (when possible) by making a **POST** call</span></span> 
 

## <a name="powershell-sample"></a><span data-ttu-id="061aa-154">PowerShell Sample</span><span class="sxs-lookup"><span data-stu-id="061aa-154">PowerShell Sample</span></span> 

<span data-ttu-id="061aa-155">The following sample reads the metadata server for scheduled events and approves the events.</span><span class="sxs-lookup"><span data-stu-id="061aa-155">The following sample reads the metadata server for scheduled events and approves the events.</span></span>

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


## <a name="c-sample"></a><span data-ttu-id="061aa-156">C\# Sample</span><span class="sxs-lookup"><span data-stu-id="061aa-156">C\# Sample</span></span> 
<span data-ttu-id="061aa-157">The following sample is of a client surfacing APIs to communicate with the Metadata Service</span><span class="sxs-lookup"><span data-stu-id="061aa-157">The following sample is of a client surfacing APIs to communicate with the Metadata Service</span></span>
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
<span data-ttu-id="061aa-158">Scheduled Events could be parsed using the following data structures</span><span class="sxs-lookup"><span data-stu-id="061aa-158">Scheduled Events could be parsed using the following data structures</span></span> 

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

<span data-ttu-id="061aa-159">A Sample Program using the client to retrieve, handle, and acknowledge events:</span><span class="sxs-lookup"><span data-stu-id="061aa-159">A Sample Program using the client to retrieve, handle, and acknowledge events:</span></span>   

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

## <a name="python-sample"></a><span data-ttu-id="061aa-160">Python Sample</span><span class="sxs-lookup"><span data-stu-id="061aa-160">Python Sample</span></span> 

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
## <a name="next-steps"></a><span data-ttu-id="061aa-161">Next Steps</span><span class="sxs-lookup"><span data-stu-id="061aa-161">Next Steps</span></span> 
[<span data-ttu-id="061aa-162">Planned maintenance for virtual machines in Azure</span><span class="sxs-lookup"><span data-stu-id="061aa-162">Planned maintenance for virtual machines in Azure</span></span>](linux/planned-maintenance.md)
