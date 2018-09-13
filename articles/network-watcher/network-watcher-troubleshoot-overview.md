---
title: Introduction to resource troubleshooting in Azure Network Watcher | Microsoft Docs
description: This page provides an overview of the Network Watcher resource troubleshooting capabilities
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: c1145cd6-d1cf-4770-b1cc-eaf0464cc315
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 335d246f3130ffd14069460ef123278236813251
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554765"
---
# <a name="introduction-to-resource-troubleshooting-in-azure-network-watcher"></a><span data-ttu-id="e07c1-103">Introduction to resource troubleshooting in Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="e07c1-103">Introduction to resource troubleshooting in Azure Network Watcher</span></span>

<span data-ttu-id="e07c1-104">Virtual Network Gateways provide connectivity between on-premises resources and other virtual networks within Azure.</span><span class="sxs-lookup"><span data-stu-id="e07c1-104">Virtual Network Gateways provide connectivity between on-premises resources and other virtual networks within Azure.</span></span> <span data-ttu-id="e07c1-105">Monitoring these gateways and their Connections is critical to ensuring communication is not broken.</span><span class="sxs-lookup"><span data-stu-id="e07c1-105">Monitoring these gateways and their Connections is critical to ensuring communication is not broken.</span></span> <span data-ttu-id="e07c1-106">Network Watcher provides the capability to troubleshoot Virtual Network Gateways and Connections.</span><span class="sxs-lookup"><span data-stu-id="e07c1-106">Network Watcher provides the capability to troubleshoot Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="e07c1-107">This can be called by PowerShell, CLI, or REST API.</span><span class="sxs-lookup"><span data-stu-id="e07c1-107">This can be called by PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="e07c1-108">When called, Network Watcher diagnoses the health of the virtual network gateway or connection and return the appropriate results.</span><span class="sxs-lookup"><span data-stu-id="e07c1-108">When called, Network Watcher diagnoses the health of the virtual network gateway or connection and return the appropriate results.</span></span> <span data-ttu-id="e07c1-109">This request is a long running transaction, the results are returned once the diagnosis is complete.</span><span class="sxs-lookup"><span data-stu-id="e07c1-109">This request is a long running transaction, the results are returned once the diagnosis is complete.</span></span>

## <a name="results"></a><span data-ttu-id="e07c1-110">Results</span><span class="sxs-lookup"><span data-stu-id="e07c1-110">Results</span></span>

<span data-ttu-id="e07c1-111">The preliminary results returned give an overall picture of the health of the resource.</span><span class="sxs-lookup"><span data-stu-id="e07c1-111">The preliminary results returned give an overall picture of the health of the resource.</span></span> <span data-ttu-id="e07c1-112">Deeper information can be provided for resources as shown in the following section:</span><span class="sxs-lookup"><span data-stu-id="e07c1-112">Deeper information can be provided for resources as shown in the following section:</span></span>

<span data-ttu-id="e07c1-113">The following list is the values returned with the troubleshoot API:</span><span class="sxs-lookup"><span data-stu-id="e07c1-113">The following list is the values returned with the troubleshoot API:</span></span>

* <span data-ttu-id="e07c1-114">**startTime** - This value is the time the troubleshoot API call started.</span><span class="sxs-lookup"><span data-stu-id="e07c1-114">**startTime** - This value is the time the troubleshoot API call started.</span></span>
* <span data-ttu-id="e07c1-115">**endTime** - This value is the time when the troubleshooting ended.</span><span class="sxs-lookup"><span data-stu-id="e07c1-115">**endTime** - This value is the time when the troubleshooting ended.</span></span>
* <span data-ttu-id="e07c1-116">**code** - This value is UnHealthy, if there is a single diagnosis failure.</span><span class="sxs-lookup"><span data-stu-id="e07c1-116">**code** - This value is UnHealthy, if there is a single diagnosis failure.</span></span>
* <span data-ttu-id="e07c1-117">**results** - Results is a collection of results returned on the Connection or the virtual network gateway.</span><span class="sxs-lookup"><span data-stu-id="e07c1-117">**results** - Results is a collection of results returned on the Connection or the virtual network gateway.</span></span>
    * <span data-ttu-id="e07c1-118">**id** - This value is the fault type.</span><span class="sxs-lookup"><span data-stu-id="e07c1-118">**id** - This value is the fault type.</span></span>
    * <span data-ttu-id="e07c1-119">**summary** - This value is a summary of the fault.</span><span class="sxs-lookup"><span data-stu-id="e07c1-119">**summary** - This value is a summary of the fault.</span></span>
    * <span data-ttu-id="e07c1-120">**detailed** - This value provides a detailed description of the fault.</span><span class="sxs-lookup"><span data-stu-id="e07c1-120">**detailed** - This value provides a detailed description of the fault.</span></span>
    * <span data-ttu-id="e07c1-121">**recommendedActions** - This property is a collection of recommended actions to take.</span><span class="sxs-lookup"><span data-stu-id="e07c1-121">**recommendedActions** - This property is a collection of recommended actions to take.</span></span>
      * <span data-ttu-id="e07c1-122">**actionText** - This value contains the text describing what action to take.</span><span class="sxs-lookup"><span data-stu-id="e07c1-122">**actionText** - This value contains the text describing what action to take.</span></span>
      * <span data-ttu-id="e07c1-123">**actionUri** - This value provides the URI to documentation on how to act.</span><span class="sxs-lookup"><span data-stu-id="e07c1-123">**actionUri** - This value provides the URI to documentation on how to act.</span></span>
      * <span data-ttu-id="e07c1-124">**actionUriText** - This value is a short description of the action text.</span><span class="sxs-lookup"><span data-stu-id="e07c1-124">**actionUriText** - This value is a short description of the action text.</span></span>

<span data-ttu-id="e07c1-125">The following tables show the different fault types (id under results from the preceding list) that are available and if the fault creates logs.</span><span class="sxs-lookup"><span data-stu-id="e07c1-125">The following tables show the different fault types (id under results from the preceding list) that are available and if the fault creates logs.</span></span>

### <a name="gateway"></a><span data-ttu-id="e07c1-126">Gateway</span><span class="sxs-lookup"><span data-stu-id="e07c1-126">Gateway</span></span>

| <span data-ttu-id="e07c1-127">Fault Type</span><span class="sxs-lookup"><span data-stu-id="e07c1-127">Fault Type</span></span> | <span data-ttu-id="e07c1-128">Reason</span><span class="sxs-lookup"><span data-stu-id="e07c1-128">Reason</span></span> | <span data-ttu-id="e07c1-129">Log</span><span class="sxs-lookup"><span data-stu-id="e07c1-129">Log</span></span>|
|---|---|---|
| <span data-ttu-id="e07c1-130">NoFault</span><span class="sxs-lookup"><span data-stu-id="e07c1-130">NoFault</span></span> | <span data-ttu-id="e07c1-131">When no error is detected.</span><span class="sxs-lookup"><span data-stu-id="e07c1-131">When no error is detected.</span></span> |<span data-ttu-id="e07c1-132">Yes</span><span class="sxs-lookup"><span data-stu-id="e07c1-132">Yes</span></span>|
| <span data-ttu-id="e07c1-133">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="e07c1-133">GatewayNotFound</span></span> | <span data-ttu-id="e07c1-134">Cannot find Gateway or Gateway is not provisioned.</span><span class="sxs-lookup"><span data-stu-id="e07c1-134">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="e07c1-135">No</span><span class="sxs-lookup"><span data-stu-id="e07c1-135">No</span></span>|
| <span data-ttu-id="e07c1-136">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="e07c1-136">PlannedMaintenance</span></span> |  <span data-ttu-id="e07c1-137">Gateway instance is under maintenance.</span><span class="sxs-lookup"><span data-stu-id="e07c1-137">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="e07c1-138">No</span><span class="sxs-lookup"><span data-stu-id="e07c1-138">No</span></span>|
| <span data-ttu-id="e07c1-139">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="e07c1-139">UserDrivenUpdate</span></span> | <span data-ttu-id="e07c1-140">When a user update is in progress.</span><span class="sxs-lookup"><span data-stu-id="e07c1-140">When a user update is in progress.</span></span> <span data-ttu-id="e07c1-141">This could be a resize operation.</span><span class="sxs-lookup"><span data-stu-id="e07c1-141">This could be a resize operation.</span></span> | <span data-ttu-id="e07c1-142">No</span><span class="sxs-lookup"><span data-stu-id="e07c1-142">No</span></span> |
| <span data-ttu-id="e07c1-143">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="e07c1-143">VipUnResponsive</span></span> | <span data-ttu-id="e07c1-144">Cannot reach the primary instance of the Gateway.</span><span class="sxs-lookup"><span data-stu-id="e07c1-144">Cannot reach the primary instance of the Gateway.</span></span> <span data-ttu-id="e07c1-145">This happens when the health probe fails.</span><span class="sxs-lookup"><span data-stu-id="e07c1-145">This happens when the health probe fails.</span></span> | <span data-ttu-id="e07c1-146">No</span><span class="sxs-lookup"><span data-stu-id="e07c1-146">No</span></span> |
| <span data-ttu-id="e07c1-147">PlatformInActive</span><span class="sxs-lookup"><span data-stu-id="e07c1-147">PlatformInActive</span></span> | <span data-ttu-id="e07c1-148">There is an issue with the platform.</span><span class="sxs-lookup"><span data-stu-id="e07c1-148">There is an issue with the platform.</span></span> | <span data-ttu-id="e07c1-149">No</span><span class="sxs-lookup"><span data-stu-id="e07c1-149">No</span></span>|
| <span data-ttu-id="e07c1-150">ServiceNotRunning</span><span class="sxs-lookup"><span data-stu-id="e07c1-150">ServiceNotRunning</span></span> | <span data-ttu-id="e07c1-151">The underlying service is not running.</span><span class="sxs-lookup"><span data-stu-id="e07c1-151">The underlying service is not running.</span></span> | <span data-ttu-id="e07c1-152">No</span><span class="sxs-lookup"><span data-stu-id="e07c1-152">No</span></span>|
| <span data-ttu-id="e07c1-153">NoConnectionsFoundForGateway</span><span class="sxs-lookup"><span data-stu-id="e07c1-153">NoConnectionsFoundForGateway</span></span> | <span data-ttu-id="e07c1-154">No Connections exists on the gateway.</span><span class="sxs-lookup"><span data-stu-id="e07c1-154">No Connections exists on the gateway.</span></span> <span data-ttu-id="e07c1-155">This is only a warning.</span><span class="sxs-lookup"><span data-stu-id="e07c1-155">This is only a warning.</span></span>| <span data-ttu-id="e07c1-156">No</span><span class="sxs-lookup"><span data-stu-id="e07c1-156">No</span></span>|
| <span data-ttu-id="e07c1-157">ConnectionsNotConnected</span><span class="sxs-lookup"><span data-stu-id="e07c1-157">ConnectionsNotConnected</span></span> | <span data-ttu-id="e07c1-158">No Connections are not connected.</span><span class="sxs-lookup"><span data-stu-id="e07c1-158">No Connections are not connected.</span></span> <span data-ttu-id="e07c1-159">This is only a warning.</span><span class="sxs-lookup"><span data-stu-id="e07c1-159">This is only a warning.</span></span>| <span data-ttu-id="e07c1-160">Yes</span><span class="sxs-lookup"><span data-stu-id="e07c1-160">Yes</span></span>|
| <span data-ttu-id="e07c1-161">GatewayCPUUsageExceeded</span><span class="sxs-lookup"><span data-stu-id="e07c1-161">GatewayCPUUsageExceeded</span></span> | <span data-ttu-id="e07c1-162">The current Gateway CPU usage is > 95%.</span><span class="sxs-lookup"><span data-stu-id="e07c1-162">The current Gateway CPU usage is > 95%.</span></span> | <span data-ttu-id="e07c1-163">Yes</span><span class="sxs-lookup"><span data-stu-id="e07c1-163">Yes</span></span> |

### <a name="connection"></a><span data-ttu-id="e07c1-164">Connection</span><span class="sxs-lookup"><span data-stu-id="e07c1-164">Connection</span></span>

| <span data-ttu-id="e07c1-165">Fault Type</span><span class="sxs-lookup"><span data-stu-id="e07c1-165">Fault Type</span></span> | <span data-ttu-id="e07c1-166">Reason</span><span class="sxs-lookup"><span data-stu-id="e07c1-166">Reason</span></span> | <span data-ttu-id="e07c1-167">Log</span><span class="sxs-lookup"><span data-stu-id="e07c1-167">Log</span></span>|
|---|---|---|
| <span data-ttu-id="e07c1-168">NoFault</span><span class="sxs-lookup"><span data-stu-id="e07c1-168">NoFault</span></span> | <span data-ttu-id="e07c1-169">When no error is detected.</span><span class="sxs-lookup"><span data-stu-id="e07c1-169">When no error is detected.</span></span> |<span data-ttu-id="e07c1-170">Yes</span><span class="sxs-lookup"><span data-stu-id="e07c1-170">Yes</span></span>|
| <span data-ttu-id="e07c1-171">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="e07c1-171">GatewayNotFound</span></span> | <span data-ttu-id="e07c1-172">Cannot find Gateway or Gateway is not provisioned.</span><span class="sxs-lookup"><span data-stu-id="e07c1-172">Cannot find Gateway or Gateway is not provisioned.</span></span> |<span data-ttu-id="e07c1-173">No</span><span class="sxs-lookup"><span data-stu-id="e07c1-173">No</span></span>|
| <span data-ttu-id="e07c1-174">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="e07c1-174">PlannedMaintenance</span></span> | <span data-ttu-id="e07c1-175">Gateway instance is under maintenance.</span><span class="sxs-lookup"><span data-stu-id="e07c1-175">Gateway instance is under maintenance.</span></span>  |<span data-ttu-id="e07c1-176">No</span><span class="sxs-lookup"><span data-stu-id="e07c1-176">No</span></span>|
| <span data-ttu-id="e07c1-177">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="e07c1-177">UserDrivenUpdate</span></span> | <span data-ttu-id="e07c1-178">When a user update is in progress.</span><span class="sxs-lookup"><span data-stu-id="e07c1-178">When a user update is in progress.</span></span> <span data-ttu-id="e07c1-179">This could be a resize operation.</span><span class="sxs-lookup"><span data-stu-id="e07c1-179">This could be a resize operation.</span></span>  | <span data-ttu-id="e07c1-180">No</span><span class="sxs-lookup"><span data-stu-id="e07c1-180">No</span></span> |
| <span data-ttu-id="e07c1-181">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="e07c1-181">VipUnResponsive</span></span> | <span data-ttu-id="e07c1-182">Cannot reach the primary instance of the Gateway.</span><span class="sxs-lookup"><span data-stu-id="e07c1-182">Cannot reach the primary instance of the Gateway.</span></span> <span data-ttu-id="e07c1-183">It happens when the health probe fails.</span><span class="sxs-lookup"><span data-stu-id="e07c1-183">It happens when the health probe fails.</span></span> | <span data-ttu-id="e07c1-184">No</span><span class="sxs-lookup"><span data-stu-id="e07c1-184">No</span></span> |
| <span data-ttu-id="e07c1-185">ConnectionEntityNotFound</span><span class="sxs-lookup"><span data-stu-id="e07c1-185">ConnectionEntityNotFound</span></span> | <span data-ttu-id="e07c1-186">Connection configuration is missing.</span><span class="sxs-lookup"><span data-stu-id="e07c1-186">Connection configuration is missing.</span></span> | <span data-ttu-id="e07c1-187">No</span><span class="sxs-lookup"><span data-stu-id="e07c1-187">No</span></span> |
| <span data-ttu-id="e07c1-188">ConnectionIsMarkedDisconnected</span><span class="sxs-lookup"><span data-stu-id="e07c1-188">ConnectionIsMarkedDisconnected</span></span> | <span data-ttu-id="e07c1-189">The Connection is marked "disconnected".</span><span class="sxs-lookup"><span data-stu-id="e07c1-189">The Connection is marked "disconnected".</span></span> |<span data-ttu-id="e07c1-190">No</span><span class="sxs-lookup"><span data-stu-id="e07c1-190">No</span></span>|
| <span data-ttu-id="e07c1-191">ConnectionNotConfiguredOnGateway</span><span class="sxs-lookup"><span data-stu-id="e07c1-191">ConnectionNotConfiguredOnGateway</span></span> | <span data-ttu-id="e07c1-192">The underlying service does not have the Connection configured.</span><span class="sxs-lookup"><span data-stu-id="e07c1-192">The underlying service does not have the Connection configured.</span></span> | <span data-ttu-id="e07c1-193">Yes</span><span class="sxs-lookup"><span data-stu-id="e07c1-193">Yes</span></span> |
| <span data-ttu-id="e07c1-194">ConnectionMarkedStandy</span><span class="sxs-lookup"><span data-stu-id="e07c1-194">ConnectionMarkedStandy</span></span> | <span data-ttu-id="e07c1-195">The underlying service is marked as standby.</span><span class="sxs-lookup"><span data-stu-id="e07c1-195">The underlying service is marked as standby.</span></span>| <span data-ttu-id="e07c1-196">Yes</span><span class="sxs-lookup"><span data-stu-id="e07c1-196">Yes</span></span>|
| <span data-ttu-id="e07c1-197">Authentication</span><span class="sxs-lookup"><span data-stu-id="e07c1-197">Authentication</span></span> | <span data-ttu-id="e07c1-198">Preshared Key mismatch.</span><span class="sxs-lookup"><span data-stu-id="e07c1-198">Preshared Key mismatch.</span></span> | <span data-ttu-id="e07c1-199">Yes</span><span class="sxs-lookup"><span data-stu-id="e07c1-199">Yes</span></span>|
| <span data-ttu-id="e07c1-200">PeerReachability</span><span class="sxs-lookup"><span data-stu-id="e07c1-200">PeerReachability</span></span> | <span data-ttu-id="e07c1-201">The peer gateway is not reachable.</span><span class="sxs-lookup"><span data-stu-id="e07c1-201">The peer gateway is not reachable.</span></span> | <span data-ttu-id="e07c1-202">Yes</span><span class="sxs-lookup"><span data-stu-id="e07c1-202">Yes</span></span>|
| <span data-ttu-id="e07c1-203">IkePolicyMismatch</span><span class="sxs-lookup"><span data-stu-id="e07c1-203">IkePolicyMismatch</span></span> | <span data-ttu-id="e07c1-204">The peer gateway has IKE policies that are not supported by Azure.</span><span class="sxs-lookup"><span data-stu-id="e07c1-204">The peer gateway has IKE policies that are not supported by Azure.</span></span> | <span data-ttu-id="e07c1-205">Yes</span><span class="sxs-lookup"><span data-stu-id="e07c1-205">Yes</span></span>|
| <span data-ttu-id="e07c1-206">WfpParse Error</span><span class="sxs-lookup"><span data-stu-id="e07c1-206">WfpParse Error</span></span> | <span data-ttu-id="e07c1-207">An error occurred parsing the WFP log.</span><span class="sxs-lookup"><span data-stu-id="e07c1-207">An error occurred parsing the WFP log.</span></span> |<span data-ttu-id="e07c1-208">Yes</span><span class="sxs-lookup"><span data-stu-id="e07c1-208">Yes</span></span>|


## <a name="log-files"></a><span data-ttu-id="e07c1-209">Log files</span><span class="sxs-lookup"><span data-stu-id="e07c1-209">Log files</span></span>

<span data-ttu-id="e07c1-210">The resource troubleshooting log files are stored in a storage account after resource troubleshooting is finished.</span><span class="sxs-lookup"><span data-stu-id="e07c1-210">The resource troubleshooting log files are stored in a storage account after resource troubleshooting is finished.</span></span> <span data-ttu-id="e07c1-211">The following image shows the example contents of a call that resulted in an error.</span><span class="sxs-lookup"><span data-stu-id="e07c1-211">The following image shows the example contents of a call that resulted in an error.</span></span>

![zip file][1]

> [!NOTE]
> <span data-ttu-id="e07c1-213">In some cases, only a subset of the logs files is written to storage.</span><span class="sxs-lookup"><span data-stu-id="e07c1-213">In some cases, only a subset of the logs files is written to storage.</span></span>

<span data-ttu-id="e07c1-214">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="e07c1-214">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="e07c1-215">Another tool that can be used is Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="e07c1-215">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="e07c1-216">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="e07c1-216">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

### <a name="connectionstatstxt"></a><span data-ttu-id="e07c1-217">ConnectionStats.txt</span><span class="sxs-lookup"><span data-stu-id="e07c1-217">ConnectionStats.txt</span></span>

<span data-ttu-id="e07c1-218">The **ConnectionStats.txt** file contains overall stats of the Connection, including ingress and egress bytes, Connection status, and the time the Connection was established.</span><span class="sxs-lookup"><span data-stu-id="e07c1-218">The **ConnectionStats.txt** file contains overall stats of the Connection, including ingress and egress bytes, Connection status, and the time the Connection was established.</span></span>

> [!NOTE]
> <span data-ttu-id="e07c1-219">If the call to the troubleshooting API returns healthy, the only thing returned in the zip file is a **ConnectionStats.txt** file.</span><span class="sxs-lookup"><span data-stu-id="e07c1-219">If the call to the troubleshooting API returns healthy, the only thing returned in the zip file is a **ConnectionStats.txt** file.</span></span>

<span data-ttu-id="e07c1-220">The contents of this file are similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="e07c1-220">The contents of this file are similar to the following example:</span></span>

```
Connectivity State : Connected
Remote Tunnel Endpoint :
Ingress Bytes (since last connected) : 288 B
Egress Bytes (Since last connected) : 288 B
Connected Since : 2/1/2017 8:22:06 PM
```

### <a name="cpustatstxt"></a><span data-ttu-id="e07c1-221">CPUStats.txt</span><span class="sxs-lookup"><span data-stu-id="e07c1-221">CPUStats.txt</span></span>

<span data-ttu-id="e07c1-222">The **CPUStats.txt** file contains CPU usage and memory available at the time of testing.</span><span class="sxs-lookup"><span data-stu-id="e07c1-222">The **CPUStats.txt** file contains CPU usage and memory available at the time of testing.</span></span>  <span data-ttu-id="e07c1-223">The contents of this file is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="e07c1-223">The contents of this file is similar to the following example:</span></span>

```
Current CPU Usage : 0 % Current Memory Available : 641 MBs
```

### <a name="ikeerrorstxt"></a><span data-ttu-id="e07c1-224">IKEErrors.txt</span><span class="sxs-lookup"><span data-stu-id="e07c1-224">IKEErrors.txt</span></span>

<span data-ttu-id="e07c1-225">The **IKEErrors.txt** file contains any IKE errors that were found during monitoring.</span><span class="sxs-lookup"><span data-stu-id="e07c1-225">The **IKEErrors.txt** file contains any IKE errors that were found during monitoring.</span></span>

<span data-ttu-id="e07c1-226">The following example shows the contents of an IKEErrors.txt file.</span><span class="sxs-lookup"><span data-stu-id="e07c1-226">The following example shows the contents of an IKEErrors.txt file.</span></span> <span data-ttu-id="e07c1-227">Your errors may be different depending on the issue.</span><span class="sxs-lookup"><span data-stu-id="e07c1-227">Your errors may be different depending on the issue.</span></span>

```
Error: Authentication failed. Check shared key. Check crypto. Check lifetimes. 
     based on log : Peer failed with Windows error 13801(ERROR_IPSEC_IKE_AUTH_FAIL)
Error: On-prem device sent invalid payload. 
     based on log : IkeFindPayloadInPacket failed with Windows error 13843(ERROR_IPSEC_IKE_INVALID_PAYLOAD)
```

### <a name="scrubbed-wfpdiagtxt"></a><span data-ttu-id="e07c1-228">Scrubbed-wfpdiag.txt</span><span class="sxs-lookup"><span data-stu-id="e07c1-228">Scrubbed-wfpdiag.txt</span></span>

<span data-ttu-id="e07c1-229">The **Scrubbed-wfpdiag.txt** log file contains the wfp log.</span><span class="sxs-lookup"><span data-stu-id="e07c1-229">The **Scrubbed-wfpdiag.txt** log file contains the wfp log.</span></span> <span data-ttu-id="e07c1-230">This log contains logging of packet drop and IKE/AuthIP failures.</span><span class="sxs-lookup"><span data-stu-id="e07c1-230">This log contains logging of packet drop and IKE/AuthIP failures.</span></span>

<span data-ttu-id="e07c1-231">The following example shows the contents of the Scrubbed-wfpdiag.txt file.</span><span class="sxs-lookup"><span data-stu-id="e07c1-231">The following example shows the contents of the Scrubbed-wfpdiag.txt file.</span></span> <span data-ttu-id="e07c1-232">In this example, the shared key of a Connection was not correct as can be seen from the 3rd line from the bottom.</span><span class="sxs-lookup"><span data-stu-id="e07c1-232">In this example, the shared key of a Connection was not correct as can be seen from the 3rd line from the bottom.</span></span> <span data-ttu-id="e07c1-233">The following example is just a snippet of the entire log, as the log can be lengthy depending on the issue.</span><span class="sxs-lookup"><span data-stu-id="e07c1-233">The following example is just a snippet of the entire log, as the log can be lengthy depending on the issue.</span></span>

```
...
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Deleted ICookie from the high priority thread pool list
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|IKE diagnostic event:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Event Header:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Timestamp: 1601-01-01T00:00:00.000Z
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Flags: 0x00000106
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Local address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    Remote address field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IP version field set
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP version: IPv4
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  IP protocol: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local address: 13.78.238.92
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote address: 52.161.24.36
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Local Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Remote Port: 0
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Application ID:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  User SID: <invalid>
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Failure type: IKE/Authip Main Mode Failure
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|Type specific info:
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure error code:0x000035e9
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|    IKE authentication credentials are unacceptable
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|
[0]0368.03A4::02/02/2017-17:36:01.496 [ikeext] 3038|52.161.24.36|  Failure point: Remote
...
```

### <a name="wfpdiagtxtsum"></a><span data-ttu-id="e07c1-234">wfpdiag.txt.sum</span><span class="sxs-lookup"><span data-stu-id="e07c1-234">wfpdiag.txt.sum</span></span>

<span data-ttu-id="e07c1-235">The **wfpdiag.txt.sum** file is a log showing the buffers and events processed.</span><span class="sxs-lookup"><span data-stu-id="e07c1-235">The **wfpdiag.txt.sum** file is a log showing the buffers and events processed.</span></span>

<span data-ttu-id="e07c1-236">The following example is the contents of a wfpdiag.txt.sum file.</span><span class="sxs-lookup"><span data-stu-id="e07c1-236">The following example is the contents of a wfpdiag.txt.sum file.</span></span>
```
Files Processed:
    C:\Resources\directory\924336c47dd045d5a246c349b8ae57f2.GatewayTenantWorker.DiagnosticsStorage\2017-02-02T17-34-23\wfpdiag.etl
Total Buffers Processed 8
Total Events  Processed 2169
Total Events  Lost      0
Total Format  Errors    0
Total Formats Unknown   486
Elapsed Time            330 sec
+-----------------------------------------------------------------------------------+
|EventCount    EventName            EventType   TMF                                 |
+-----------------------------------------------------------------------------------+
|        36    ikeext               ike_addr_utils_c844  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        12    ikeext               ike_addr_utils_c857  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|        96    ikeext               ike_addr_utils_c832  a0c064ca-d954-350a-8b2f-1a7464eef8b6|
|         6    ikeext               ike_bfe_callbacks_c133  1dc2d67f-8381-6303-e314-6c1452eeb529|
|         6    ikeext               ike_bfe_callbacks_c61  1dc2d67f-8381-6303-e314-6c1452eeb529|
|        12    ikeext               ike_sa_management_c5698  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c8447  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c494  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c642  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|         6    ikeext               ike_sa_management_c3162  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
|        12    ikeext               ike_sa_management_c3307  7857a320-42ee-6e90-d5d9-3f414e3ea2d3|
```

## <a name="next-steps"></a><span data-ttu-id="e07c1-237">Next steps</span><span class="sxs-lookup"><span data-stu-id="e07c1-237">Next steps</span></span>

<span data-ttu-id="e07c1-238">Learn how to diagnose VPN Gateways and Connections with PowerShell by visiting [Gateway troubleshooting - PowerShell](network-watcher-troubleshoot-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e07c1-238">Learn how to diagnose VPN Gateways and Connections with PowerShell by visiting [Gateway troubleshooting - PowerShell](network-watcher-troubleshoot-manage-powershell.md).</span></span>
<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-troubleshoot-overview/GatewayTenantWorkerLogs.png

