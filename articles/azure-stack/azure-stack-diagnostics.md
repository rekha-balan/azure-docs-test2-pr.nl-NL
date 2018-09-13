---
title: Diagnostics in Azure Stack | Microsoft Docs
description: How to collect log files for diagnostics in Azure Stack
services: azure-stack
documentationcenter: ''
author: adshar
manager: byronr
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/14/2017
ms.author: adshar;victorh
ms.openlocfilehash: 75b39d1622b4828c591b4a35cb97a27a51a8fa64
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563863"
---
# <a name="azure-stack-diagnostics-tools"></a><span data-ttu-id="67880-103">Azure Stack diagnostics tools</span><span class="sxs-lookup"><span data-stu-id="67880-103">Azure Stack diagnostics tools</span></span>
 
<span data-ttu-id="67880-104">Azure Stack is a large collection of components working together and interacting with each other.</span><span class="sxs-lookup"><span data-stu-id="67880-104">Azure Stack is a large collection of components working together and interacting with each other.</span></span> <span data-ttu-id="67880-105">All these components  generate their own unique logs, which means that diagnosing issues can quickly become a challenging task, especially for errors coming from multiple interacting Azure Stack components.</span><span class="sxs-lookup"><span data-stu-id="67880-105">All these components  generate their own unique logs, which means that diagnosing issues can quickly become a challenging task, especially for errors coming from multiple interacting Azure Stack components.</span></span> 

<span data-ttu-id="67880-106">Our diagnostics tools help make sure the log collection mechanism is easy and efficient.</span><span class="sxs-lookup"><span data-stu-id="67880-106">Our diagnostics tools help make sure the log collection mechanism is easy and efficient.</span></span> <span data-ttu-id="67880-107">The following diagram shows how log collection tools in Azure Stack work:</span><span class="sxs-lookup"><span data-stu-id="67880-107">The following diagram shows how log collection tools in Azure Stack work:</span></span>

![Log collection tools](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-diagnostics/image01.png)
 
 
## <a name="trace-collector"></a><span data-ttu-id="67880-109">Trace Collector</span><span class="sxs-lookup"><span data-stu-id="67880-109">Trace Collector</span></span>
 
<span data-ttu-id="67880-110">The Trace Collector is enabled by default.</span><span class="sxs-lookup"><span data-stu-id="67880-110">The Trace Collector is enabled by default.</span></span> <span data-ttu-id="67880-111">It continuously runs in the background and collects all Event Tracing for Windows (ETW) logs from component services on Azure Stack and stores them on a common local share.</span><span class="sxs-lookup"><span data-stu-id="67880-111">It continuously runs in the background and collects all Event Tracing for Windows (ETW) logs from component services on Azure Stack and stores them on a common local share.</span></span> 

<span data-ttu-id="67880-112">The following are important things to know about the Trace Collector:</span><span class="sxs-lookup"><span data-stu-id="67880-112">The following are important things to know about the Trace Collector:</span></span>
 
* <span data-ttu-id="67880-113">The Trace Collector runs continuously with default size limits.</span><span class="sxs-lookup"><span data-stu-id="67880-113">The Trace Collector runs continuously with default size limits.</span></span> <span data-ttu-id="67880-114">The default maximum size allowed for each file (200 MB) is **not** a cutoff size.</span><span class="sxs-lookup"><span data-stu-id="67880-114">The default maximum size allowed for each file (200 MB) is **not** a cutoff size.</span></span> <span data-ttu-id="67880-115">A size check occurs periodically (currently every 10 minutes) and if the current file is >= 200 MB, it is saved and a new file is generated.</span><span class="sxs-lookup"><span data-stu-id="67880-115">A size check occurs periodically (currently every 10 minutes) and if the current file is >= 200 MB, it is saved and a new file is generated.</span></span> <span data-ttu-id="67880-116">There is also an 8 GB (configurable) limit on the total file size generated per event session.</span><span class="sxs-lookup"><span data-stu-id="67880-116">There is also an 8 GB (configurable) limit on the total file size generated per event session.</span></span> <span data-ttu-id="67880-117">Once this limit is reached, the oldest files are deleted as new ones are created.</span><span class="sxs-lookup"><span data-stu-id="67880-117">Once this limit is reached, the oldest files are deleted as new ones are created.</span></span>
* <span data-ttu-id="67880-118">There is a 5-day age limit on the logs.</span><span class="sxs-lookup"><span data-stu-id="67880-118">There is a 5-day age limit on the logs.</span></span> <span data-ttu-id="67880-119">This limit is also configurable.</span><span class="sxs-lookup"><span data-stu-id="67880-119">This limit is also configurable.</span></span> 
* <span data-ttu-id="67880-120">Each component defines the trace configuration properties through a JSON file.</span><span class="sxs-lookup"><span data-stu-id="67880-120">Each component defines the trace configuration properties through a JSON file.</span></span> <span data-ttu-id="67880-121">The JSON files are stored in `C:\TraceCollector\Configuration`.</span><span class="sxs-lookup"><span data-stu-id="67880-121">The JSON files are stored in `C:\TraceCollector\Configuration`.</span></span> <span data-ttu-id="67880-122">If necessary, these files can be edited to change the age and size limits of the collected logs.</span><span class="sxs-lookup"><span data-stu-id="67880-122">If necessary, these files can be edited to change the age and size limits of the collected logs.</span></span> <span data-ttu-id="67880-123">Changes to these files require a restart of the *Microsoft Azure Stack Trace Collector* service for the changes to take effect.</span><span class="sxs-lookup"><span data-stu-id="67880-123">Changes to these files require a restart of the *Microsoft Azure Stack Trace Collector* service for the changes to take effect.</span></span>
* <span data-ttu-id="67880-124">The following example is a trace configuration JSON file for FabricRingServices Operations from the XRP VM:</span><span class="sxs-lookup"><span data-stu-id="67880-124">The following example is a trace configuration JSON file for FabricRingServices Operations from the XRP VM:</span></span> 

```
{
    "LogFile": 
    {
        "SessionName": "FabricRingServicesOperationsLogSession",
        "FileName": "\\\\SU1FileServer\\SU1_ManagementLibrary_1\\Diagnostics\\FabricRingServices\\Operations\\AzureStack.Common.Infrastructure.Operations.etl",
        "RollTimeStamp": "00:00:00",
        "MaxDaysOfFiles": "5",
        "MaxSizeInMB": "200",
        "TotalSizeInMB": "5120"
    },
    "EventSources":
    [
        {"Name": "Microsoft-AzureStack-Common-Infrastructure-ResourceManager" },
        {"Name": "Microsoft-OperationManager-EventSource" },
        {"Name": "Microsoft-Operation-EventSource" }
    ]
}
```

* <span data-ttu-id="67880-125">**MaxDaysOfFiles**</span><span class="sxs-lookup"><span data-stu-id="67880-125">**MaxDaysOfFiles**</span></span>

    <span data-ttu-id="67880-126">This parameter controls the age of files to keep.</span><span class="sxs-lookup"><span data-stu-id="67880-126">This parameter controls the age of files to keep.</span></span> <span data-ttu-id="67880-127">Older log files are deleted.</span><span class="sxs-lookup"><span data-stu-id="67880-127">Older log files are deleted.</span></span>
* <span data-ttu-id="67880-128">**MaxSizeInMB**</span><span class="sxs-lookup"><span data-stu-id="67880-128">**MaxSizeInMB**</span></span>

    <span data-ttu-id="67880-129">This parameter controls the size threshold for a single file.</span><span class="sxs-lookup"><span data-stu-id="67880-129">This parameter controls the size threshold for a single file.</span></span> <span data-ttu-id="67880-130">If the size is reached, a new .etl file is created.</span><span class="sxs-lookup"><span data-stu-id="67880-130">If the size is reached, a new .etl file is created.</span></span>
* <span data-ttu-id="67880-131">**TotalSizeInMB**</span><span class="sxs-lookup"><span data-stu-id="67880-131">**TotalSizeInMB**</span></span>

    <span data-ttu-id="67880-132">This parameter controls the total size of the .etl files generated from an event session.</span><span class="sxs-lookup"><span data-stu-id="67880-132">This parameter controls the total size of the .etl files generated from an event session.</span></span> <span data-ttu-id="67880-133">If the total file size is greater than this parameter value, older files are deleted.</span><span class="sxs-lookup"><span data-stu-id="67880-133">If the total file size is greater than this parameter value, older files are deleted.</span></span>
  
## <a name="log-collection-tool"></a><span data-ttu-id="67880-134">Log collection tool</span><span class="sxs-lookup"><span data-stu-id="67880-134">Log collection tool</span></span>
 
<span data-ttu-id="67880-135">The PowerShell command `Get-AzureStackLogs` can be used to collect logs from all the components  in an Azure Stack environment.</span><span class="sxs-lookup"><span data-stu-id="67880-135">The PowerShell command `Get-AzureStackLogs` can be used to collect logs from all the components  in an Azure Stack environment.</span></span> <span data-ttu-id="67880-136">It saves them in zip files in a user defined location.</span><span class="sxs-lookup"><span data-stu-id="67880-136">It saves them in zip files in a user defined location.</span></span> <span data-ttu-id="67880-137">If our technical support team needs your logs to help troubleshoot an issue, they may ask you to run this tool.</span><span class="sxs-lookup"><span data-stu-id="67880-137">If our technical support team needs your logs to help troubleshoot an issue, they may ask you to run this tool.</span></span>

> [!CAUTION]
> <span data-ttu-id="67880-138">These log files may contain personally identifiable information (PII).</span><span class="sxs-lookup"><span data-stu-id="67880-138">These log files may contain personally identifiable information (PII).</span></span> <span data-ttu-id="67880-139">Take this into account before you publicly post any log files.</span><span class="sxs-lookup"><span data-stu-id="67880-139">Take this into account before you publicly post any log files.</span></span>
 
<span data-ttu-id="67880-140">We currently collect the following log types:</span><span class="sxs-lookup"><span data-stu-id="67880-140">We currently collect the following log types:</span></span>
*   <span data-ttu-id="67880-141">**Azure Stack deployment logs**</span><span class="sxs-lookup"><span data-stu-id="67880-141">**Azure Stack deployment logs**</span></span>
*   <span data-ttu-id="67880-142">**Windows event logs**</span><span class="sxs-lookup"><span data-stu-id="67880-142">**Windows event logs**</span></span>
*   <span data-ttu-id="67880-143">**Panther logs**</span><span class="sxs-lookup"><span data-stu-id="67880-143">**Panther logs**</span></span>

     <span data-ttu-id="67880-144">To troubleshoot VM creation issues.</span><span class="sxs-lookup"><span data-stu-id="67880-144">To troubleshoot VM creation issues.</span></span>
*   <span data-ttu-id="67880-145">**Cluster logs**</span><span class="sxs-lookup"><span data-stu-id="67880-145">**Cluster logs**</span></span>
*   <span data-ttu-id="67880-146">**Storage diagnostic logs**</span><span class="sxs-lookup"><span data-stu-id="67880-146">**Storage diagnostic logs**</span></span>
*   <span data-ttu-id="67880-147">**ETW logs**</span><span class="sxs-lookup"><span data-stu-id="67880-147">**ETW logs**</span></span>

    <span data-ttu-id="67880-148">These are collected by the Trace Collector and stored in a share from where `Get-AzureStackLogs` retrieves them.</span><span class="sxs-lookup"><span data-stu-id="67880-148">These are collected by the Trace Collector and stored in a share from where `Get-AzureStackLogs` retrieves them.</span></span>
 
<span data-ttu-id="67880-149">To identify all the logs that get collected from all the components, refer to the `<Logs>` tags in the customer configuration file located at `C:\EceStore\<Guid>\<GuidWithMaxFileSize>`.</span><span class="sxs-lookup"><span data-stu-id="67880-149">To identify all the logs that get collected from all the components, refer to the `<Logs>` tags in the customer configuration file located at `C:\EceStore\<Guid>\<GuidWithMaxFileSize>`.</span></span>
 
### <a name="to-run-get-azurestacklogs"></a><span data-ttu-id="67880-150">To run Get-AzureStackLogs</span><span class="sxs-lookup"><span data-stu-id="67880-150">To run Get-AzureStackLogs</span></span>
1.  <span data-ttu-id="67880-151">Log in as AzureStack\AzureStackAdmin on the host.</span><span class="sxs-lookup"><span data-stu-id="67880-151">Log in as AzureStack\AzureStackAdmin on the host.</span></span>
2.  <span data-ttu-id="67880-152">Open a PowerShell window as an administrator.</span><span class="sxs-lookup"><span data-stu-id="67880-152">Open a PowerShell window as an administrator.</span></span>
3.  <span data-ttu-id="67880-153">Run the following commands to import the PowerShell modules:</span><span class="sxs-lookup"><span data-stu-id="67880-153">Run the following commands to import the PowerShell modules:</span></span>

    -   `cd C:\CloudDeployment\AzureStackDiagnostics\Microsoft.AzureStack.Diagnostics.DataCollection`

    -   `Import-Module .\Microsoft.AzureStack.Diagnostics.DataCollection.psd1`

4.  <span data-ttu-id="67880-154">Run `Get-AzureStackLogs`.</span><span class="sxs-lookup"><span data-stu-id="67880-154">Run `Get-AzureStackLogs`.</span></span>  

    <span data-ttu-id="67880-155">**Examples**</span><span class="sxs-lookup"><span data-stu-id="67880-155">**Examples**</span></span>

    - <span data-ttu-id="67880-156">Collect all logs for all roles:</span><span class="sxs-lookup"><span data-stu-id="67880-156">Collect all logs for all roles:</span></span>

        `Get-AzureStackLogs -OutputPath C:\AzureStackLogs`

    - <span data-ttu-id="67880-157">Collect logs from VirtualMachines and BareMetal roles:</span><span class="sxs-lookup"><span data-stu-id="67880-157">Collect logs from VirtualMachines and BareMetal roles:</span></span>

        `Get-AzureStackLogs -OutputPath C:\AzureStackLogs -FilterByRole VirtualMachines,BareMetal`

    - <span data-ttu-id="67880-158">Collect logs from VirtualMachines and BareMetal roles, with date filtering for log files for the past 8 hours:</span><span class="sxs-lookup"><span data-stu-id="67880-158">Collect logs from VirtualMachines and BareMetal roles, with date filtering for log files for the past 8 hours:</span></span>

        `Get-AzureStackLogs -OutputPath C:\AzureStackLogs -FilterByRole VirtualMachines,BareMetal -FromDate (Get-Date).AddHours(-8) -ToDate (Get-Date)`

<span data-ttu-id="67880-159">If the `FromDate` and `ToDate` parameters are not specified, logs are collected for the past 4 hours by default.</span><span class="sxs-lookup"><span data-stu-id="67880-159">If the `FromDate` and `ToDate` parameters are not specified, logs are collected for the past 4 hours by default.</span></span>

<span data-ttu-id="67880-160">Currently, you can use the `FilterByRole` parameter to filter log collection by the following roles:</span><span class="sxs-lookup"><span data-stu-id="67880-160">Currently, you can use the `FilterByRole` parameter to filter log collection by the following roles:</span></span>

|   |   |   |
| - | - | - |
| `ACSMigrationService`     | `ACSMonitoringService`   | `ACSSettingsService` |
| `ACS`                     | `ACSFabric`              | `ACSFrontEnd`        |
| `ACSTableMaster`          | `ACSTableServer`         | `ACSWac`             |
| `ADFS`                    | `ASAppGateway`           | `BareMetal`          |
| `BRP`                     | `CA`                     | `CPI`                |
| `CRP`                     | `DeploymentMachine`      | `DHCP`               |
|`Domain`                   | `ECE`                    | `ECESeedRing`        |        
| `FabricRing`              | `FabricRingServices`     | `FRP`                |
|` Gateway`                 | `HealthMonitoring`       | `HRP`                |               
| `IBC`                     | `InfraServiceController` | `KeyVaultAdminResourceProvider`|
| `KeyVaultControlPlane`    | `KeyVaultDataPlane`      | `NC`                 |            
| `NonPrivilegedAppGateway` | `NRP`                    | `SeedRing`           |
| `SeedRingServices`        | `SLB`                    | `SQL`                |     
| `SRP`                     | `Storage`                | `StorageController`  |
| `URP`                     | `UsageBridge`            | `VirtualMachines`    |  
| `WAS`                     | `WASPUBLIC`              | `WDS`                |


<span data-ttu-id="67880-161">A few things to note:</span><span class="sxs-lookup"><span data-stu-id="67880-161">A few things to note:</span></span>

* <span data-ttu-id="67880-162">This command takes some time for log collection based on which role logs are collected.</span><span class="sxs-lookup"><span data-stu-id="67880-162">This command takes some time for log collection based on which role logs are collected.</span></span> <span data-ttu-id="67880-163">Contributing factors include the time duration specified for log collection, and the numbers of nodes in the Azure Stack environment.</span><span class="sxs-lookup"><span data-stu-id="67880-163">Contributing factors include the time duration specified for log collection, and the numbers of nodes in the Azure Stack environment.</span></span>
* <span data-ttu-id="67880-164">After log collection completes, check the new folder created in the `-OutputPath` parameter specified in the command.</span><span class="sxs-lookup"><span data-stu-id="67880-164">After log collection completes, check the new folder created in the `-OutputPath` parameter specified in the command.</span></span>
* <span data-ttu-id="67880-165">A file called `Get-AzureStackLogs_Output.log` is created in the folder containing the zip files and includes the command output, which can be used for troubleshooting any failures in log collection.</span><span class="sxs-lookup"><span data-stu-id="67880-165">A file called `Get-AzureStackLogs_Output.log` is created in the folder containing the zip files and includes the command output, which can be used for troubleshooting any failures in log collection.</span></span>
* <span data-ttu-id="67880-166">Each role has its logs inside an individual zip file.</span><span class="sxs-lookup"><span data-stu-id="67880-166">Each role has its logs inside an individual zip file.</span></span> 
* <span data-ttu-id="67880-167">To investigate a specific failure, logs may be needed from more than one component.</span><span class="sxs-lookup"><span data-stu-id="67880-167">To investigate a specific failure, logs may be needed from more than one component.</span></span>
    -   <span data-ttu-id="67880-168">System and Event logs for all infrastructure VMs are collected in the *VirtualMachines* role.</span><span class="sxs-lookup"><span data-stu-id="67880-168">System and Event logs for all infrastructure VMs are collected in the *VirtualMachines* role.</span></span>
    -   <span data-ttu-id="67880-169">System and Event logs for all hosts are collected in the *BareMetal* role.</span><span class="sxs-lookup"><span data-stu-id="67880-169">System and Event logs for all hosts are collected in the *BareMetal* role.</span></span>
    -   <span data-ttu-id="67880-170">Failover Cluster and Hyper-V event logs are collected in the *Storage* role.</span><span class="sxs-lookup"><span data-stu-id="67880-170">Failover Cluster and Hyper-V event logs are collected in the *Storage* role.</span></span>
    -   <span data-ttu-id="67880-171">ACS logs are collected in the *Storage* and *ACS* roles.</span><span class="sxs-lookup"><span data-stu-id="67880-171">ACS logs are collected in the *Storage* and *ACS* roles.</span></span>
* <span data-ttu-id="67880-172">For more details, you can refer to the customer configuration file.</span><span class="sxs-lookup"><span data-stu-id="67880-172">For more details, you can refer to the customer configuration file.</span></span> <span data-ttu-id="67880-173">Investigate the `<Logs>` tags for the different roles.</span><span class="sxs-lookup"><span data-stu-id="67880-173">Investigate the `<Logs>` tags for the different roles.</span></span>

> [!NOTE]
> <span data-ttu-id="67880-174">We are enforcing size and age limits to the logs collected as it is essential to ensure efficient utilization of your storage space to make sure it doesn't get flooded with logs.</span><span class="sxs-lookup"><span data-stu-id="67880-174">We are enforcing size and age limits to the logs collected as it is essential to ensure efficient utilization of your storage space to make sure it doesn't get flooded with logs.</span></span> <span data-ttu-id="67880-175">Having said that, when diagnosing a problem you will often need logs that might not exist anymore due to these limits being enforced.</span><span class="sxs-lookup"><span data-stu-id="67880-175">Having said that, when diagnosing a problem you will often need logs that might not exist anymore due to these limits being enforced.</span></span> <span data-ttu-id="67880-176">Hence, it is **highly recommended** that you offload your logs to an external storage space (a storage account in public Azure, an additional on-prem storage device etc.) every 8 to 12 hours and keep them there for 1 - 3 months depending on your requirements.</span><span class="sxs-lookup"><span data-stu-id="67880-176">Hence, it is **highly recommended** that you offload your logs to an external storage space (a storage account in public Azure, an additional on-prem storage device etc.) every 8 to 12 hours and keep them there for 1 - 3 months depending on your requirements.</span></span>


## <a name="next-steps"></a><span data-ttu-id="67880-177">Next steps</span><span class="sxs-lookup"><span data-stu-id="67880-177">Next steps</span></span>
[<span data-ttu-id="67880-178">Microsoft Azure Stack troubleshooting</span><span class="sxs-lookup"><span data-stu-id="67880-178">Microsoft Azure Stack troubleshooting</span></span>](azure-stack-troubleshooting.md)

