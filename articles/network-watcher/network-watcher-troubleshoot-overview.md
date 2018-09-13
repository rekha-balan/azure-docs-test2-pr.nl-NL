---
title: Introduction to resource troubleshooting in Azure Network Watcher | Microsoft Docs
description: This page provides an overview of the Network Watcher resource troubleshooting capabilities
services: network-watcher
documentationcenter: na
author: jimdial
manager: jeconnoc
editor: ''
ms.assetid: c1145cd6-d1cf-4770-b1cc-eaf0464cc315
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: jdial
ms.openlocfilehash: 2f8a41834c1451d80c53cfed4bae3b7e36281702
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44805641"
---
# <a name="introduction-to-resource-troubleshooting-in-azure-network-watcher"></a><span data-ttu-id="52e09-103">Introduction to resource troubleshooting in Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="52e09-103">Introduction to resource troubleshooting in Azure Network Watcher</span></span>

<span data-ttu-id="52e09-104">Virtual Network Gateways provide connectivity between on-premises resources and other virtual networks within Azure.</span><span class="sxs-lookup"><span data-stu-id="52e09-104">Virtual Network Gateways provide connectivity between on-premises resources and other virtual networks within Azure.</span></span> <span data-ttu-id="52e09-105">Monitoring gateways and their connections are critical to ensuring communication is not broken.</span><span class="sxs-lookup"><span data-stu-id="52e09-105">Monitoring gateways and their connections are critical to ensuring communication is not broken.</span></span> <span data-ttu-id="52e09-106">Network Watcher provides the capability to troubleshoot gateways and connections.</span><span class="sxs-lookup"><span data-stu-id="52e09-106">Network Watcher provides the capability to troubleshoot gateways and connections.</span></span> <span data-ttu-id="52e09-107">The capability can be called through the portal, PowerShell, Azure CLI, or REST API.</span><span class="sxs-lookup"><span data-stu-id="52e09-107">The capability can be called through the portal, PowerShell, Azure CLI, or REST API.</span></span> <span data-ttu-id="52e09-108">When called, Network Watcher diagnoses the health of the gateway, or connection, and returns the appropriate results.</span><span class="sxs-lookup"><span data-stu-id="52e09-108">When called, Network Watcher diagnoses the health of the gateway, or connection, and returns the appropriate results.</span></span> <span data-ttu-id="52e09-109">The request is a long running transaction.</span><span class="sxs-lookup"><span data-stu-id="52e09-109">The request is a long running transaction.</span></span> <span data-ttu-id="52e09-110">The results are returned once the diagnosis is complete.</span><span class="sxs-lookup"><span data-stu-id="52e09-110">The results are returned once the diagnosis is complete.</span></span>

![portal][2]

## <a name="results"></a><span data-ttu-id="52e09-112">Results</span><span class="sxs-lookup"><span data-stu-id="52e09-112">Results</span></span>

<span data-ttu-id="52e09-113">The preliminary results returned give an overall picture of the health of the resource.</span><span class="sxs-lookup"><span data-stu-id="52e09-113">The preliminary results returned give an overall picture of the health of the resource.</span></span> <span data-ttu-id="52e09-114">Deeper information can be provided for resources as shown in the following section:</span><span class="sxs-lookup"><span data-stu-id="52e09-114">Deeper information can be provided for resources as shown in the following section:</span></span>

<span data-ttu-id="52e09-115">The following list is the values returned with the troubleshoot API:</span><span class="sxs-lookup"><span data-stu-id="52e09-115">The following list is the values returned with the troubleshoot API:</span></span>

* <span data-ttu-id="52e09-116">**startTime** - This value is the time the troubleshoot API call started.</span><span class="sxs-lookup"><span data-stu-id="52e09-116">**startTime** - This value is the time the troubleshoot API call started.</span></span>
* <span data-ttu-id="52e09-117">**endTime** - This value is the time when the troubleshooting ended.</span><span class="sxs-lookup"><span data-stu-id="52e09-117">**endTime** - This value is the time when the troubleshooting ended.</span></span>
* <span data-ttu-id="52e09-118">**code** - This value is UnHealthy, if there is a single diagnosis failure.</span><span class="sxs-lookup"><span data-stu-id="52e09-118">**code** - This value is UnHealthy, if there is a single diagnosis failure.</span></span>
* <span data-ttu-id="52e09-119">**results** - Results is a collection of results returned on the Connection or the virtual network gateway.</span><span class="sxs-lookup"><span data-stu-id="52e09-119">**results** - Results is a collection of results returned on the Connection or the virtual network gateway.</span></span>
    * <span data-ttu-id="52e09-120">**id** - This value is the fault type.</span><span class="sxs-lookup"><span data-stu-id="52e09-120">**id** - This value is the fault type.</span></span>
    * <span data-ttu-id="52e09-121">**summary** - This value is a summary of the fault.</span><span class="sxs-lookup"><span data-stu-id="52e09-121">**summary** - This value is a summary of the fault.</span></span>
    * <span data-ttu-id="52e09-122">**detailed** - This value provides a detailed description of the fault.</span><span class="sxs-lookup"><span data-stu-id="52e09-122">**detailed** - This value provides a detailed description of the fault.</span></span>
    * <span data-ttu-id="52e09-123">**recommendedActions** - This property is a collection of recommended actions to take.</span><span class="sxs-lookup"><span data-stu-id="52e09-123">**recommendedActions** - This property is a collection of recommended actions to take.</span></span>
      * <span data-ttu-id="52e09-124">**actionText** - This value contains the text describing what action to take.</span><span class="sxs-lookup"><span data-stu-id="52e09-124">**actionText** - This value contains the text describing what action to take.</span></span>
      * <span data-ttu-id="52e09-125">**actionUri** - This value provides the URI to documentation on how to act.</span><span class="sxs-lookup"><span data-stu-id="52e09-125">**actionUri** - This value provides the URI to documentation on how to act.</span></span>
      * <span data-ttu-id="52e09-126">**actionUriText** - This value is a short description of the action text.</span><span class="sxs-lookup"><span data-stu-id="52e09-126">**actionUriText** - This value is a short description of the action text.</span></span>

<span data-ttu-id="52e09-127">The following tables show the different fault types (id under results from the preceding list) that are available and if the fault creates logs.</span><span class="sxs-lookup"><span data-stu-id="52e09-127">The following tables show the different fault types (id under results from the preceding list) that are available and if the fault creates logs.</span></span>

### <a name="gateway"></a><span data-ttu-id="52e09-128">Gateway</span><span class="sxs-lookup"><span data-stu-id="52e09-128">Gateway</span></span>

| <span data-ttu-id="52e09-129">Fault Type</span><span class="sxs-lookup"><span data-stu-id="52e09-129">Fault Type</span></span> | <span data-ttu-id="52e09-130">Reason</span><span class="sxs-lookup"><span data-stu-id="52e09-130">Reason</span></span> | <span data-ttu-id="52e09-131">Log</span><span class="sxs-lookup"><span data-stu-id="52e09-131">Log</span></span>|
|---|---|---|
| <span data-ttu-id="52e09-132">NoFault</span><span class="sxs-lookup"><span data-stu-id="52e09-132">NoFault</span></span> | <span data-ttu-id="52e09-133">When no error is detected</span><span class="sxs-lookup"><span data-stu-id="52e09-133">When no error is detected</span></span> |<span data-ttu-id="52e09-134">Yes</span><span class="sxs-lookup"><span data-stu-id="52e09-134">Yes</span></span>|
| <span data-ttu-id="52e09-135">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="52e09-135">GatewayNotFound</span></span> | <span data-ttu-id="52e09-136">Cannot find gateway or gateway is not provisioned</span><span class="sxs-lookup"><span data-stu-id="52e09-136">Cannot find gateway or gateway is not provisioned</span></span> |<span data-ttu-id="52e09-137">No</span><span class="sxs-lookup"><span data-stu-id="52e09-137">No</span></span>|
| <span data-ttu-id="52e09-138">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="52e09-138">PlannedMaintenance</span></span> |  <span data-ttu-id="52e09-139">Gateway instance is under maintenance</span><span class="sxs-lookup"><span data-stu-id="52e09-139">Gateway instance is under maintenance</span></span>  |<span data-ttu-id="52e09-140">No</span><span class="sxs-lookup"><span data-stu-id="52e09-140">No</span></span>|
| <span data-ttu-id="52e09-141">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="52e09-141">UserDrivenUpdate</span></span> | <span data-ttu-id="52e09-142">This fault occurs when a user update is in progress.</span><span class="sxs-lookup"><span data-stu-id="52e09-142">This fault occurs when a user update is in progress.</span></span> <span data-ttu-id="52e09-143">The update could be a resize operation.</span><span class="sxs-lookup"><span data-stu-id="52e09-143">The update could be a resize operation.</span></span> | <span data-ttu-id="52e09-144">No</span><span class="sxs-lookup"><span data-stu-id="52e09-144">No</span></span> |
| <span data-ttu-id="52e09-145">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="52e09-145">VipUnResponsive</span></span> | <span data-ttu-id="52e09-146">This fault occurs when the primary instance of the gateway can't be reached due to a health probe failure.</span><span class="sxs-lookup"><span data-stu-id="52e09-146">This fault occurs when the primary instance of the gateway can't be reached due to a health probe failure.</span></span> | <span data-ttu-id="52e09-147">No</span><span class="sxs-lookup"><span data-stu-id="52e09-147">No</span></span> |
| <span data-ttu-id="52e09-148">PlatformInActive</span><span class="sxs-lookup"><span data-stu-id="52e09-148">PlatformInActive</span></span> | <span data-ttu-id="52e09-149">There is an issue with the platform.</span><span class="sxs-lookup"><span data-stu-id="52e09-149">There is an issue with the platform.</span></span> | <span data-ttu-id="52e09-150">No</span><span class="sxs-lookup"><span data-stu-id="52e09-150">No</span></span>|
| <span data-ttu-id="52e09-151">ServiceNotRunning</span><span class="sxs-lookup"><span data-stu-id="52e09-151">ServiceNotRunning</span></span> | <span data-ttu-id="52e09-152">The underlying service is not running.</span><span class="sxs-lookup"><span data-stu-id="52e09-152">The underlying service is not running.</span></span> | <span data-ttu-id="52e09-153">No</span><span class="sxs-lookup"><span data-stu-id="52e09-153">No</span></span>|
| <span data-ttu-id="52e09-154">NoConnectionsFoundForGateway</span><span class="sxs-lookup"><span data-stu-id="52e09-154">NoConnectionsFoundForGateway</span></span> | <span data-ttu-id="52e09-155">No connections exist on the gateway.</span><span class="sxs-lookup"><span data-stu-id="52e09-155">No connections exist on the gateway.</span></span> <span data-ttu-id="52e09-156">This fault is only a warning.</span><span class="sxs-lookup"><span data-stu-id="52e09-156">This fault is only a warning.</span></span>| <span data-ttu-id="52e09-157">No</span><span class="sxs-lookup"><span data-stu-id="52e09-157">No</span></span>|
| <span data-ttu-id="52e09-158">ConnectionsNotConnected</span><span class="sxs-lookup"><span data-stu-id="52e09-158">ConnectionsNotConnected</span></span> | <span data-ttu-id="52e09-159">Connections are not connected.</span><span class="sxs-lookup"><span data-stu-id="52e09-159">Connections are not connected.</span></span> <span data-ttu-id="52e09-160">This fault is only a warning.</span><span class="sxs-lookup"><span data-stu-id="52e09-160">This fault is only a warning.</span></span>| <span data-ttu-id="52e09-161">Yes</span><span class="sxs-lookup"><span data-stu-id="52e09-161">Yes</span></span>|
| <span data-ttu-id="52e09-162">GatewayCPUUsageExceeded</span><span class="sxs-lookup"><span data-stu-id="52e09-162">GatewayCPUUsageExceeded</span></span> | <span data-ttu-id="52e09-163">The current gateway CPU usage is > 95%.</span><span class="sxs-lookup"><span data-stu-id="52e09-163">The current gateway CPU usage is > 95%.</span></span> | <span data-ttu-id="52e09-164">Yes</span><span class="sxs-lookup"><span data-stu-id="52e09-164">Yes</span></span> |

### <a name="connection"></a><span data-ttu-id="52e09-165">Connection</span><span class="sxs-lookup"><span data-stu-id="52e09-165">Connection</span></span>

| <span data-ttu-id="52e09-166">Fault Type</span><span class="sxs-lookup"><span data-stu-id="52e09-166">Fault Type</span></span> | <span data-ttu-id="52e09-167">Reason</span><span class="sxs-lookup"><span data-stu-id="52e09-167">Reason</span></span> | <span data-ttu-id="52e09-168">Log</span><span class="sxs-lookup"><span data-stu-id="52e09-168">Log</span></span>|
|---|---|---|
| <span data-ttu-id="52e09-169">NoFault</span><span class="sxs-lookup"><span data-stu-id="52e09-169">NoFault</span></span> | <span data-ttu-id="52e09-170">When no error is detected</span><span class="sxs-lookup"><span data-stu-id="52e09-170">When no error is detected</span></span> |<span data-ttu-id="52e09-171">Yes</span><span class="sxs-lookup"><span data-stu-id="52e09-171">Yes</span></span>|
| <span data-ttu-id="52e09-172">GatewayNotFound</span><span class="sxs-lookup"><span data-stu-id="52e09-172">GatewayNotFound</span></span> | <span data-ttu-id="52e09-173">Cannot find gateway or gateway is not provisioned</span><span class="sxs-lookup"><span data-stu-id="52e09-173">Cannot find gateway or gateway is not provisioned</span></span> |<span data-ttu-id="52e09-174">No</span><span class="sxs-lookup"><span data-stu-id="52e09-174">No</span></span>|
| <span data-ttu-id="52e09-175">PlannedMaintenance</span><span class="sxs-lookup"><span data-stu-id="52e09-175">PlannedMaintenance</span></span> | <span data-ttu-id="52e09-176">Gateway instance is under maintenance</span><span class="sxs-lookup"><span data-stu-id="52e09-176">Gateway instance is under maintenance</span></span>  |<span data-ttu-id="52e09-177">No</span><span class="sxs-lookup"><span data-stu-id="52e09-177">No</span></span>|
| <span data-ttu-id="52e09-178">UserDrivenUpdate</span><span class="sxs-lookup"><span data-stu-id="52e09-178">UserDrivenUpdate</span></span> | <span data-ttu-id="52e09-179">This fault occurs when a user update is in progress.</span><span class="sxs-lookup"><span data-stu-id="52e09-179">This fault occurs when a user update is in progress.</span></span> <span data-ttu-id="52e09-180">The update could be a resize operation.</span><span class="sxs-lookup"><span data-stu-id="52e09-180">The update could be a resize operation.</span></span>  | <span data-ttu-id="52e09-181">No</span><span class="sxs-lookup"><span data-stu-id="52e09-181">No</span></span> |
| <span data-ttu-id="52e09-182">VipUnResponsive</span><span class="sxs-lookup"><span data-stu-id="52e09-182">VipUnResponsive</span></span> | <span data-ttu-id="52e09-183">This fault occurs when the primary instance of the gateway can't be reached due to a health probe failure.</span><span class="sxs-lookup"><span data-stu-id="52e09-183">This fault occurs when the primary instance of the gateway can't be reached due to a health probe failure.</span></span> | <span data-ttu-id="52e09-184">No</span><span class="sxs-lookup"><span data-stu-id="52e09-184">No</span></span> |
| <span data-ttu-id="52e09-185">ConnectionEntityNotFound</span><span class="sxs-lookup"><span data-stu-id="52e09-185">ConnectionEntityNotFound</span></span> | <span data-ttu-id="52e09-186">Connection configuration is missing</span><span class="sxs-lookup"><span data-stu-id="52e09-186">Connection configuration is missing</span></span> | <span data-ttu-id="52e09-187">No</span><span class="sxs-lookup"><span data-stu-id="52e09-187">No</span></span> |
| <span data-ttu-id="52e09-188">ConnectionIsMarkedDisconnected</span><span class="sxs-lookup"><span data-stu-id="52e09-188">ConnectionIsMarkedDisconnected</span></span> | <span data-ttu-id="52e09-189">The connection is marked "disconnected"</span><span class="sxs-lookup"><span data-stu-id="52e09-189">The connection is marked "disconnected"</span></span> |<span data-ttu-id="52e09-190">No</span><span class="sxs-lookup"><span data-stu-id="52e09-190">No</span></span>|
| <span data-ttu-id="52e09-191">ConnectionNotConfiguredOnGateway</span><span class="sxs-lookup"><span data-stu-id="52e09-191">ConnectionNotConfiguredOnGateway</span></span> | <span data-ttu-id="52e09-192">The underlying service does not have the connection configured.</span><span class="sxs-lookup"><span data-stu-id="52e09-192">The underlying service does not have the connection configured.</span></span> | <span data-ttu-id="52e09-193">Yes</span><span class="sxs-lookup"><span data-stu-id="52e09-193">Yes</span></span> |
| <span data-ttu-id="52e09-194">ConnectionMarkedStandy</span><span class="sxs-lookup"><span data-stu-id="52e09-194">ConnectionMarkedStandy</span></span> | <span data-ttu-id="52e09-195">The underlying service is marked as standby.</span><span class="sxs-lookup"><span data-stu-id="52e09-195">The underlying service is marked as standby.</span></span>| <span data-ttu-id="52e09-196">Yes</span><span class="sxs-lookup"><span data-stu-id="52e09-196">Yes</span></span>|
| <span data-ttu-id="52e09-197">Authentication</span><span class="sxs-lookup"><span data-stu-id="52e09-197">Authentication</span></span> | <span data-ttu-id="52e09-198">Preshared key mismatch</span><span class="sxs-lookup"><span data-stu-id="52e09-198">Preshared key mismatch</span></span> | <span data-ttu-id="52e09-199">Yes</span><span class="sxs-lookup"><span data-stu-id="52e09-199">Yes</span></span>|
| <span data-ttu-id="52e09-200">PeerReachability</span><span class="sxs-lookup"><span data-stu-id="52e09-200">PeerReachability</span></span> | <span data-ttu-id="52e09-201">The peer gateway is not reachable.</span><span class="sxs-lookup"><span data-stu-id="52e09-201">The peer gateway is not reachable.</span></span> | <span data-ttu-id="52e09-202">Yes</span><span class="sxs-lookup"><span data-stu-id="52e09-202">Yes</span></span>|
| <span data-ttu-id="52e09-203">IkePolicyMismatch</span><span class="sxs-lookup"><span data-stu-id="52e09-203">IkePolicyMismatch</span></span> | <span data-ttu-id="52e09-204">The peer gateway has IKE policies that are not supported by Azure.</span><span class="sxs-lookup"><span data-stu-id="52e09-204">The peer gateway has IKE policies that are not supported by Azure.</span></span> | <span data-ttu-id="52e09-205">Yes</span><span class="sxs-lookup"><span data-stu-id="52e09-205">Yes</span></span>|
| <span data-ttu-id="52e09-206">WfpParse Error</span><span class="sxs-lookup"><span data-stu-id="52e09-206">WfpParse Error</span></span> | <span data-ttu-id="52e09-207">An error occurred parsing the WFP log.</span><span class="sxs-lookup"><span data-stu-id="52e09-207">An error occurred parsing the WFP log.</span></span> |<span data-ttu-id="52e09-208">Yes</span><span class="sxs-lookup"><span data-stu-id="52e09-208">Yes</span></span>|

## <a name="supported-gateway-types"></a><span data-ttu-id="52e09-209">Supported Gateway types</span><span class="sxs-lookup"><span data-stu-id="52e09-209">Supported Gateway types</span></span>

<span data-ttu-id="52e09-210">The following table lists which gateways and connections are supported with Network Watcher troubleshooting:</span><span class="sxs-lookup"><span data-stu-id="52e09-210">The following table lists which gateways and connections are supported with Network Watcher troubleshooting:</span></span>

|  |  |
|---------|---------|
|<span data-ttu-id="52e09-211">**Gateway types**</span><span class="sxs-lookup"><span data-stu-id="52e09-211">**Gateway types**</span></span>   |         |
|<span data-ttu-id="52e09-212">VPN</span><span class="sxs-lookup"><span data-stu-id="52e09-212">VPN</span></span>      | <span data-ttu-id="52e09-213">Supported</span><span class="sxs-lookup"><span data-stu-id="52e09-213">Supported</span></span>        |
|<span data-ttu-id="52e09-214">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="52e09-214">ExpressRoute</span></span> | <span data-ttu-id="52e09-215">Not Supported</span><span class="sxs-lookup"><span data-stu-id="52e09-215">Not Supported</span></span> |
|<span data-ttu-id="52e09-216">**VPN types**</span><span class="sxs-lookup"><span data-stu-id="52e09-216">**VPN types**</span></span> | |
|<span data-ttu-id="52e09-217">Route Based</span><span class="sxs-lookup"><span data-stu-id="52e09-217">Route Based</span></span> | <span data-ttu-id="52e09-218">Supported</span><span class="sxs-lookup"><span data-stu-id="52e09-218">Supported</span></span>|
|<span data-ttu-id="52e09-219">Policy Based</span><span class="sxs-lookup"><span data-stu-id="52e09-219">Policy Based</span></span> | <span data-ttu-id="52e09-220">Not Supported</span><span class="sxs-lookup"><span data-stu-id="52e09-220">Not Supported</span></span>|
|<span data-ttu-id="52e09-221">**Connection types**</span><span class="sxs-lookup"><span data-stu-id="52e09-221">**Connection types**</span></span>||
|<span data-ttu-id="52e09-222">IPSec</span><span class="sxs-lookup"><span data-stu-id="52e09-222">IPSec</span></span>| <span data-ttu-id="52e09-223">Supported</span><span class="sxs-lookup"><span data-stu-id="52e09-223">Supported</span></span>|
|<span data-ttu-id="52e09-224">VNet2Vnet</span><span class="sxs-lookup"><span data-stu-id="52e09-224">VNet2Vnet</span></span>| <span data-ttu-id="52e09-225">Supported</span><span class="sxs-lookup"><span data-stu-id="52e09-225">Supported</span></span>|
|<span data-ttu-id="52e09-226">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="52e09-226">ExpressRoute</span></span>| <span data-ttu-id="52e09-227">Not Supported</span><span class="sxs-lookup"><span data-stu-id="52e09-227">Not Supported</span></span>|
|<span data-ttu-id="52e09-228">VPNClient</span><span class="sxs-lookup"><span data-stu-id="52e09-228">VPNClient</span></span>| <span data-ttu-id="52e09-229">Not Supported</span><span class="sxs-lookup"><span data-stu-id="52e09-229">Not Supported</span></span>|

## <a name="log-files"></a><span data-ttu-id="52e09-230">Log files</span><span class="sxs-lookup"><span data-stu-id="52e09-230">Log files</span></span>

<span data-ttu-id="52e09-231">The resource troubleshooting log files are stored in a storage account after resource troubleshooting is finished.</span><span class="sxs-lookup"><span data-stu-id="52e09-231">The resource troubleshooting log files are stored in a storage account after resource troubleshooting is finished.</span></span> <span data-ttu-id="52e09-232">The following image shows the example contents of a call that resulted in an error.</span><span class="sxs-lookup"><span data-stu-id="52e09-232">The following image shows the example contents of a call that resulted in an error.</span></span>

![zip file][1]

> [!NOTE]
> <span data-ttu-id="52e09-234">In some cases, only a subset of the logs files is written to storage.</span><span class="sxs-lookup"><span data-stu-id="52e09-234">In some cases, only a subset of the logs files is written to storage.</span></span>

<span data-ttu-id="52e09-235">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="52e09-235">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="52e09-236">Another tool that can be used is Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="52e09-236">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="52e09-237">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="52e09-237">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

### <a name="connectionstatstxt"></a><span data-ttu-id="52e09-238">ConnectionStats.txt</span><span class="sxs-lookup"><span data-stu-id="52e09-238">ConnectionStats.txt</span></span>

<span data-ttu-id="52e09-239">The **ConnectionStats.txt** file contains overall stats of the Connection, including ingress and egress bytes, Connection status, and the time the Connection was established.</span><span class="sxs-lookup"><span data-stu-id="52e09-239">The **ConnectionStats.txt** file contains overall stats of the Connection, including ingress and egress bytes, Connection status, and the time the Connection was established.</span></span>

> [!NOTE]
> <span data-ttu-id="52e09-240">If the call to the troubleshooting API returns healthy, the only thing returned in the zip file is a **ConnectionStats.txt** file.</span><span class="sxs-lookup"><span data-stu-id="52e09-240">If the call to the troubleshooting API returns healthy, the only thing returned in the zip file is a **ConnectionStats.txt** file.</span></span>

<span data-ttu-id="52e09-241">The contents of this file are similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="52e09-241">The contents of this file are similar to the following example:</span></span>

```
Connectivity State : Connected
Remote Tunnel Endpoint :
Ingress Bytes (since last connected) : 288 B
Egress Bytes (Since last connected) : 288 B
Connected Since : 2/1/2017 8:22:06 PM
```

### <a name="cpustatstxt"></a><span data-ttu-id="52e09-242">CPUStats.txt</span><span class="sxs-lookup"><span data-stu-id="52e09-242">CPUStats.txt</span></span>

<span data-ttu-id="52e09-243">The **CPUStats.txt** file contains CPU usage and memory available at the time of testing.</span><span class="sxs-lookup"><span data-stu-id="52e09-243">The **CPUStats.txt** file contains CPU usage and memory available at the time of testing.</span></span>  <span data-ttu-id="52e09-244">The contents of this file is similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="52e09-244">The contents of this file is similar to the following example:</span></span>

```
Current CPU Usage : 0 % Current Memory Available : 641 MBs
```

### <a name="ikeerrorstxt"></a><span data-ttu-id="52e09-245">IKEErrors.txt</span><span class="sxs-lookup"><span data-stu-id="52e09-245">IKEErrors.txt</span></span>

<span data-ttu-id="52e09-246">The **IKEErrors.txt** file contains any IKE errors that were found during monitoring.</span><span class="sxs-lookup"><span data-stu-id="52e09-246">The **IKEErrors.txt** file contains any IKE errors that were found during monitoring.</span></span>

<span data-ttu-id="52e09-247">The following example shows the contents of an IKEErrors.txt file.</span><span class="sxs-lookup"><span data-stu-id="52e09-247">The following example shows the contents of an IKEErrors.txt file.</span></span> <span data-ttu-id="52e09-248">Your errors may be different depending on the issue.</span><span class="sxs-lookup"><span data-stu-id="52e09-248">Your errors may be different depending on the issue.</span></span>

```
Error: Authentication failed. Check shared key. Check crypto. Check lifetimes. 
     based on log : Peer failed with Windows error 13801(ERROR_IPSEC_IKE_AUTH_FAIL)
Error: On-prem device sent invalid payload. 
     based on log : IkeFindPayloadInPacket failed with Windows error 13843(ERROR_IPSEC_IKE_INVALID_PAYLOAD)
```

### <a name="scrubbed-wfpdiagtxt"></a><span data-ttu-id="52e09-249">Scrubbed-wfpdiag.txt</span><span class="sxs-lookup"><span data-stu-id="52e09-249">Scrubbed-wfpdiag.txt</span></span>

<span data-ttu-id="52e09-250">The **Scrubbed-wfpdiag.txt** log file contains the wfp log.</span><span class="sxs-lookup"><span data-stu-id="52e09-250">The **Scrubbed-wfpdiag.txt** log file contains the wfp log.</span></span> <span data-ttu-id="52e09-251">This log contains logging of packet drop and IKE/AuthIP failures.</span><span class="sxs-lookup"><span data-stu-id="52e09-251">This log contains logging of packet drop and IKE/AuthIP failures.</span></span>

<span data-ttu-id="52e09-252">The following example shows the contents of the Scrubbed-wfpdiag.txt file.</span><span class="sxs-lookup"><span data-stu-id="52e09-252">The following example shows the contents of the Scrubbed-wfpdiag.txt file.</span></span> <span data-ttu-id="52e09-253">In this example, the shared key of a Connection was not correct as can be seen from the third line from the bottom.</span><span class="sxs-lookup"><span data-stu-id="52e09-253">In this example, the shared key of a Connection was not correct as can be seen from the third line from the bottom.</span></span> <span data-ttu-id="52e09-254">The following example is just a snippet of the entire log, as the log can be lengthy depending on the issue.</span><span class="sxs-lookup"><span data-stu-id="52e09-254">The following example is just a snippet of the entire log, as the log can be lengthy depending on the issue.</span></span>

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

### <a name="wfpdiagtxtsum"></a><span data-ttu-id="52e09-255">wfpdiag.txt.sum</span><span class="sxs-lookup"><span data-stu-id="52e09-255">wfpdiag.txt.sum</span></span>

<span data-ttu-id="52e09-256">The **wfpdiag.txt.sum** file is a log showing the buffers and events processed.</span><span class="sxs-lookup"><span data-stu-id="52e09-256">The **wfpdiag.txt.sum** file is a log showing the buffers and events processed.</span></span>

<span data-ttu-id="52e09-257">The following example is the contents of a wfpdiag.txt.sum file.</span><span class="sxs-lookup"><span data-stu-id="52e09-257">The following example is the contents of a wfpdiag.txt.sum file.</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="52e09-258">Next steps</span><span class="sxs-lookup"><span data-stu-id="52e09-258">Next steps</span></span>

<span data-ttu-id="52e09-259">To learn how to diagnose a problem with a gateway or gateway connection, see [Diagnose communication problems between networks](diagnose-communication-problem-between-networks.md).</span><span class="sxs-lookup"><span data-stu-id="52e09-259">To learn how to diagnose a problem with a gateway or gateway connection, see [Diagnose communication problems between networks](diagnose-communication-problem-between-networks.md).</span></span>
<!--Image references-->

[1]: ./media/network-watcher-troubleshoot-overview/GatewayTenantWorkerLogs.png
[2]: ./media/network-watcher-troubleshoot-overview/portal.png
