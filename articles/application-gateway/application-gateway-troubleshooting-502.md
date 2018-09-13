---
title: Troubleshoot Application Gateway Bad Gateway (502) errors | Microsoft Docs
description: Learn how to troubleshoot Application Gateway 502 errors
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: ''
tags: azure-resource-manager
ms.assetid: 1d431ead-d318-47d8-b3ad-9c69f7e08813
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/16/2016
ms.author: amsriva
ms.openlocfilehash: 178cd0e1c20947c952a2abb4bad253272da9fcd4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555511"
---
# <a name="troubleshooting-bad-gateway-errors-in-application-gateway"></a><span data-ttu-id="4dfd6-103">Troubleshooting bad gateway errors in Application Gateway</span><span class="sxs-lookup"><span data-stu-id="4dfd6-103">Troubleshooting bad gateway errors in Application Gateway</span></span>

## <a name="overview"></a><span data-ttu-id="4dfd6-104">Overview</span><span class="sxs-lookup"><span data-stu-id="4dfd6-104">Overview</span></span>

<span data-ttu-id="4dfd6-105">After configuring an Azure Application Gateway, one of the errors which users may encounter is "Server Error: 502 - Web server received an invalid response while acting as a gateway or proxy server".</span><span class="sxs-lookup"><span data-stu-id="4dfd6-105">After configuring an Azure Application Gateway, one of the errors which users may encounter is "Server Error: 502 - Web server received an invalid response while acting as a gateway or proxy server".</span></span> <span data-ttu-id="4dfd6-106">This error may happen due to the following main reasons:</span><span class="sxs-lookup"><span data-stu-id="4dfd6-106">This error may happen due to the following main reasons:</span></span>

* <span data-ttu-id="4dfd6-107">Azure Application Gateway's back-end pool is not configured or empty.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-107">Azure Application Gateway's back-end pool is not configured or empty.</span></span>
* <span data-ttu-id="4dfd6-108">None of the VMs or instances in VM Scale Set are healthy.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-108">None of the VMs or instances in VM Scale Set are healthy.</span></span>
* <span data-ttu-id="4dfd6-109">Back-end VMs or instances of VM Scale Set are not responding to the default health probe.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-109">Back-end VMs or instances of VM Scale Set are not responding to the default health probe.</span></span>
* <span data-ttu-id="4dfd6-110">Invalid or improper configuration of custom health probes.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-110">Invalid or improper configuration of custom health probes.</span></span>
* <span data-ttu-id="4dfd6-111">Request time out or connectivity issues with user requests.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-111">Request time out or connectivity issues with user requests.</span></span>

## <a name="empty-backendaddresspool"></a><span data-ttu-id="4dfd6-112">Empty BackendAddressPool</span><span class="sxs-lookup"><span data-stu-id="4dfd6-112">Empty BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="4dfd6-113">Cause</span><span class="sxs-lookup"><span data-stu-id="4dfd6-113">Cause</span></span>

<span data-ttu-id="4dfd6-114">If the Application Gateway has no VMs or VM Scale Set configured in the back-end address pool, it cannot route any customer request and throws a bad gateway error.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-114">If the Application Gateway has no VMs or VM Scale Set configured in the back-end address pool, it cannot route any customer request and throws a bad gateway error.</span></span>

### <a name="solution"></a><span data-ttu-id="4dfd6-115">Solution</span><span class="sxs-lookup"><span data-stu-id="4dfd6-115">Solution</span></span>

<span data-ttu-id="4dfd6-116">Ensure that the back-end address pool is not empty.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-116">Ensure that the back-end address pool is not empty.</span></span> <span data-ttu-id="4dfd6-117">This can be done either via PowerShell, CLI, or portal.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-117">This can be done either via PowerShell, CLI, or portal.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name "SampleGateway" -ResourceGroupName "ExampleResourceGroup"
```

<span data-ttu-id="4dfd6-118">The output from the preceding cmdlet should contain non-empty back-end address pool.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-118">The output from the preceding cmdlet should contain non-empty back-end address pool.</span></span> <span data-ttu-id="4dfd6-119">Following is an example where two pools are returned which are configured with FQDN or IP addresses for backend VMs.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-119">Following is an example where two pools are returned which are configured with FQDN or IP addresses for backend VMs.</span></span> <span data-ttu-id="4dfd6-120">The provisioning state of the BackendAddressPool must be 'Succeeded'.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-120">The provisioning state of the BackendAddressPool must be 'Succeeded'.</span></span>

<span data-ttu-id="4dfd6-121">BackendAddressPoolsText:</span><span class="sxs-lookup"><span data-stu-id="4dfd6-121">BackendAddressPoolsText:</span></span>

```json
[{
    "BackendAddresses": [{
        "ipAddress": "10.0.0.10",
        "ipAddress": "10.0.0.11"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool01",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool01"
}, {
    "BackendAddresses": [{
        "Fqdn": "xyx.cloudapp.net",
        "Fqdn": "abc.cloudapp.net"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool02",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool02"
}]
```

## <a name="unhealthy-instances-in-backendaddresspool"></a><span data-ttu-id="4dfd6-122">Unhealthy instances in BackendAddressPool</span><span class="sxs-lookup"><span data-stu-id="4dfd6-122">Unhealthy instances in BackendAddressPool</span></span>

### <a name="cause"></a><span data-ttu-id="4dfd6-123">Cause</span><span class="sxs-lookup"><span data-stu-id="4dfd6-123">Cause</span></span>

<span data-ttu-id="4dfd6-124">If all the instances of BackendAddressPool are unhealthy, then Application Gateway would not have any back-end to route user request to.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-124">If all the instances of BackendAddressPool are unhealthy, then Application Gateway would not have any back-end to route user request to.</span></span> <span data-ttu-id="4dfd6-125">This could also be the case when back-end instances are healthy but do not have the required application deployed.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-125">This could also be the case when back-end instances are healthy but do not have the required application deployed.</span></span>

### <a name="solution"></a><span data-ttu-id="4dfd6-126">Solution</span><span class="sxs-lookup"><span data-stu-id="4dfd6-126">Solution</span></span>

<span data-ttu-id="4dfd6-127">Ensure that the instances are healthy and the application is properly configured.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-127">Ensure that the instances are healthy and the application is properly configured.</span></span> <span data-ttu-id="4dfd6-128">Check if the back-end instances are able to respond to a ping from another VM in the same VNet.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-128">Check if the back-end instances are able to respond to a ping from another VM in the same VNet.</span></span> <span data-ttu-id="4dfd6-129">If configured with a public end point, ensure that a browser request to the web application is serviceable.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-129">If configured with a public end point, ensure that a browser request to the web application is serviceable.</span></span>

## <a name="problems-with-default-health-probe"></a><span data-ttu-id="4dfd6-130">Problems with default health probe</span><span class="sxs-lookup"><span data-stu-id="4dfd6-130">Problems with default health probe</span></span>

### <a name="cause"></a><span data-ttu-id="4dfd6-131">Cause</span><span class="sxs-lookup"><span data-stu-id="4dfd6-131">Cause</span></span>

<span data-ttu-id="4dfd6-132">502 errors can also be frequent indicators that the default health probe is not able to reach back-end VMs.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-132">502 errors can also be frequent indicators that the default health probe is not able to reach back-end VMs.</span></span> <span data-ttu-id="4dfd6-133">When an Application Gateway instance is provisioned, it automatically configures a default health probe to each BackendAddressPool using properties of the BackendHttpSetting.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-133">When an Application Gateway instance is provisioned, it automatically configures a default health probe to each BackendAddressPool using properties of the BackendHttpSetting.</span></span> <span data-ttu-id="4dfd6-134">No user input is required to set this probe.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-134">No user input is required to set this probe.</span></span> <span data-ttu-id="4dfd6-135">Specifically, when a load balancing rule is configured, an association is made between a BackendHttpSetting and BackendAddressPool.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-135">Specifically, when a load balancing rule is configured, an association is made between a BackendHttpSetting and BackendAddressPool.</span></span> <span data-ttu-id="4dfd6-136">A default probe is configured for each of these associations and Application Gateway initiates a periodic health check connection to each instance in the BackendAddressPool at the port specified in the BackendHttpSetting element.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-136">A default probe is configured for each of these associations and Application Gateway initiates a periodic health check connection to each instance in the BackendAddressPool at the port specified in the BackendHttpSetting element.</span></span> <span data-ttu-id="4dfd6-137">Following table lists the values associated with the default health probe.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-137">Following table lists the values associated with the default health probe.</span></span>

| <span data-ttu-id="4dfd6-138">Probe property</span><span class="sxs-lookup"><span data-stu-id="4dfd6-138">Probe property</span></span> | <span data-ttu-id="4dfd6-139">Value</span><span class="sxs-lookup"><span data-stu-id="4dfd6-139">Value</span></span> | <span data-ttu-id="4dfd6-140">Description</span><span class="sxs-lookup"><span data-stu-id="4dfd6-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4dfd6-141">Probe URL</span><span class="sxs-lookup"><span data-stu-id="4dfd6-141">Probe URL</span></span> |http://127.0.0.1/ |<span data-ttu-id="4dfd6-142">URL path</span><span class="sxs-lookup"><span data-stu-id="4dfd6-142">URL path</span></span> |
| <span data-ttu-id="4dfd6-143">Interval</span><span class="sxs-lookup"><span data-stu-id="4dfd6-143">Interval</span></span> |<span data-ttu-id="4dfd6-144">30</span><span class="sxs-lookup"><span data-stu-id="4dfd6-144">30</span></span> |<span data-ttu-id="4dfd6-145">Probe interval in seconds</span><span class="sxs-lookup"><span data-stu-id="4dfd6-145">Probe interval in seconds</span></span> |
| <span data-ttu-id="4dfd6-146">Time-out</span><span class="sxs-lookup"><span data-stu-id="4dfd6-146">Time-out</span></span> |<span data-ttu-id="4dfd6-147">30</span><span class="sxs-lookup"><span data-stu-id="4dfd6-147">30</span></span> |<span data-ttu-id="4dfd6-148">Probe time-out in seconds</span><span class="sxs-lookup"><span data-stu-id="4dfd6-148">Probe time-out in seconds</span></span> |
| <span data-ttu-id="4dfd6-149">Unhealthy threshold</span><span class="sxs-lookup"><span data-stu-id="4dfd6-149">Unhealthy threshold</span></span> |<span data-ttu-id="4dfd6-150">3</span><span class="sxs-lookup"><span data-stu-id="4dfd6-150">3</span></span> |<span data-ttu-id="4dfd6-151">Probe retry count.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-151">Probe retry count.</span></span> <span data-ttu-id="4dfd6-152">The back-end server is marked down after the consecutive probe failure count reaches the unhealthy threshold.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-152">The back-end server is marked down after the consecutive probe failure count reaches the unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="4dfd6-153">Solution</span><span class="sxs-lookup"><span data-stu-id="4dfd6-153">Solution</span></span>

* <span data-ttu-id="4dfd6-154">Ensure that a default site is configured and is listening at 127.0.0.1.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-154">Ensure that a default site is configured and is listening at 127.0.0.1.</span></span>
* <span data-ttu-id="4dfd6-155">If BackendHttpSetting specifies a port other than 80, the default site should be configured to listen at that port.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-155">If BackendHttpSetting specifies a port other than 80, the default site should be configured to listen at that port.</span></span>
* <span data-ttu-id="4dfd6-156">The call to http://127.0.0.1:port should return an HTTP result code of 200.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-156">The call to http://127.0.0.1:port should return an HTTP result code of 200.</span></span> <span data-ttu-id="4dfd6-157">This should be returned within the 30 sec time-out period.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-157">This should be returned within the 30 sec time-out period.</span></span>
* <span data-ttu-id="4dfd6-158">Ensure that port configured is open and that there are no firewall rules or Azure Network Security Groups, which block incoming or outgoing traffic on the port configured.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-158">Ensure that port configured is open and that there are no firewall rules or Azure Network Security Groups, which block incoming or outgoing traffic on the port configured.</span></span>
* <span data-ttu-id="4dfd6-159">If Azure classic VMs or Cloud Service is used with FQDN or Public IP, ensure that the corresponding [endpoint](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) is opened.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-159">If Azure classic VMs or Cloud Service is used with FQDN or Public IP, ensure that the corresponding [endpoint](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) is opened.</span></span>
* <span data-ttu-id="4dfd6-160">If the VM is configured via Azure Resource Manager and is outside the VNet where Application Gateway is deployed, [Network Security Group](../virtual-network/virtual-networks-nsg.md) must be configured to allow access on the desired port.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-160">If the VM is configured via Azure Resource Manager and is outside the VNet where Application Gateway is deployed, [Network Security Group](../virtual-network/virtual-networks-nsg.md) must be configured to allow access on the desired port.</span></span>

## <a name="problems-with-custom-health-probe"></a><span data-ttu-id="4dfd6-161">Problems with custom health probe</span><span class="sxs-lookup"><span data-stu-id="4dfd6-161">Problems with custom health probe</span></span>

### <a name="cause"></a><span data-ttu-id="4dfd6-162">Cause</span><span class="sxs-lookup"><span data-stu-id="4dfd6-162">Cause</span></span>

<span data-ttu-id="4dfd6-163">Custom health probes allow additional flexibility to the default probing behavior.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-163">Custom health probes allow additional flexibility to the default probing behavior.</span></span> <span data-ttu-id="4dfd6-164">When using custom probes, users can configure the probe interval, the URL, and path to test, and how many failed responses to accept before marking the back-end pool instance as unhealthy.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-164">When using custom probes, users can configure the probe interval, the URL, and path to test, and how many failed responses to accept before marking the back-end pool instance as unhealthy.</span></span> <span data-ttu-id="4dfd6-165">The following additional properties are added.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-165">The following additional properties are added.</span></span>

| <span data-ttu-id="4dfd6-166">Probe property</span><span class="sxs-lookup"><span data-stu-id="4dfd6-166">Probe property</span></span> | <span data-ttu-id="4dfd6-167">Description</span><span class="sxs-lookup"><span data-stu-id="4dfd6-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4dfd6-168">Name</span><span class="sxs-lookup"><span data-stu-id="4dfd6-168">Name</span></span> |<span data-ttu-id="4dfd6-169">Name of the probe.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-169">Name of the probe.</span></span> <span data-ttu-id="4dfd6-170">This name is used to refer to the probe in back-end HTTP settings.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-170">This name is used to refer to the probe in back-end HTTP settings.</span></span> |
| <span data-ttu-id="4dfd6-171">Protocol</span><span class="sxs-lookup"><span data-stu-id="4dfd6-171">Protocol</span></span> |<span data-ttu-id="4dfd6-172">Protocol used to send the probe.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-172">Protocol used to send the probe.</span></span> <span data-ttu-id="4dfd6-173">The probe uses the protocol defined in the back-end HTTP settings</span><span class="sxs-lookup"><span data-stu-id="4dfd6-173">The probe uses the protocol defined in the back-end HTTP settings</span></span> |
| <span data-ttu-id="4dfd6-174">Host</span><span class="sxs-lookup"><span data-stu-id="4dfd6-174">Host</span></span> |<span data-ttu-id="4dfd6-175">Host name to send the probe.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-175">Host name to send the probe.</span></span> <span data-ttu-id="4dfd6-176">Applicable only when multi-site is configured on Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-176">Applicable only when multi-site is configured on Application Gateway.</span></span> <span data-ttu-id="4dfd6-177">This is different from VM host name.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-177">This is different from VM host name.</span></span> |
| <span data-ttu-id="4dfd6-178">Path</span><span class="sxs-lookup"><span data-stu-id="4dfd6-178">Path</span></span> |<span data-ttu-id="4dfd6-179">Relative path of the probe.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-179">Relative path of the probe.</span></span> <span data-ttu-id="4dfd6-180">The valid path starts from '/'.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-180">The valid path starts from '/'.</span></span> <span data-ttu-id="4dfd6-181">The probe is sent to \<protocol\>://\<host\>:\<port\>\<path\></span><span class="sxs-lookup"><span data-stu-id="4dfd6-181">The probe is sent to \<protocol\>://\<host\>:\<port\>\<path\></span></span> |
| <span data-ttu-id="4dfd6-182">Interval</span><span class="sxs-lookup"><span data-stu-id="4dfd6-182">Interval</span></span> |<span data-ttu-id="4dfd6-183">Probe interval in seconds.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-183">Probe interval in seconds.</span></span> <span data-ttu-id="4dfd6-184">This is the time interval between two consecutive probes.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-184">This is the time interval between two consecutive probes.</span></span> |
| <span data-ttu-id="4dfd6-185">Time-out</span><span class="sxs-lookup"><span data-stu-id="4dfd6-185">Time-out</span></span> |<span data-ttu-id="4dfd6-186">Probe time-out in seconds.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-186">Probe time-out in seconds.</span></span> <span data-ttu-id="4dfd6-187">If a valid response is not received within this time-out period, the probe is marked as failed.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-187">If a valid response is not received within this time-out period, the probe is marked as failed.</span></span> |
| <span data-ttu-id="4dfd6-188">Unhealthy threshold</span><span class="sxs-lookup"><span data-stu-id="4dfd6-188">Unhealthy threshold</span></span> |<span data-ttu-id="4dfd6-189">Probe retry count.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-189">Probe retry count.</span></span> <span data-ttu-id="4dfd6-190">The back-end server is marked down after the consecutive probe failure count reaches the unhealthy threshold.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-190">The back-end server is marked down after the consecutive probe failure count reaches the unhealthy threshold.</span></span> |

### <a name="solution"></a><span data-ttu-id="4dfd6-191">Solution</span><span class="sxs-lookup"><span data-stu-id="4dfd6-191">Solution</span></span>

<span data-ttu-id="4dfd6-192">Validate that the Custom Health Probe is configured correctly as the preceding table.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-192">Validate that the Custom Health Probe is configured correctly as the preceding table.</span></span> <span data-ttu-id="4dfd6-193">In addition to the preceding troubleshooting steps, also ensure the following:</span><span class="sxs-lookup"><span data-stu-id="4dfd6-193">In addition to the preceding troubleshooting steps, also ensure the following:</span></span>

* <span data-ttu-id="4dfd6-194">Ensure that the probe is correctly specified as per the [guide](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="4dfd6-194">Ensure that the probe is correctly specified as per the [guide](application-gateway-create-probe-ps.md).</span></span>
* <span data-ttu-id="4dfd6-195">If Application Gateway is configured for a single site, by default the Host name should be specified as '127.0.0.1', unless otherwise configured in custom probe.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-195">If Application Gateway is configured for a single site, by default the Host name should be specified as '127.0.0.1', unless otherwise configured in custom probe.</span></span>
* <span data-ttu-id="4dfd6-196">Ensure that a call to http://\<host\>:\<port\>\<path\> returns an HTTP result code of 200.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-196">Ensure that a call to http://\<host\>:\<port\>\<path\> returns an HTTP result code of 200.</span></span>
* <span data-ttu-id="4dfd6-197">Ensure that Interval, Time-out and UnhealtyThreshold are within the acceptable ranges.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-197">Ensure that Interval, Time-out and UnhealtyThreshold are within the acceptable ranges.</span></span>
* <span data-ttu-id="4dfd6-198">If using an HTTPS probe, make sure that the backend server doesn't require SNI by configuring a fallback certificate on the backend server itself.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-198">If using an HTTPS probe, make sure that the backend server doesn't require SNI by configuring a fallback certificate on the backend server itself.</span></span> 
* <span data-ttu-id="4dfd6-199">Ensure that Interval, Time-out, and UnhealtyThreshold are within the acceptable ranges.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-199">Ensure that Interval, Time-out, and UnhealtyThreshold are within the acceptable ranges.</span></span>

## <a name="request-time-out"></a><span data-ttu-id="4dfd6-200">Request time out</span><span class="sxs-lookup"><span data-stu-id="4dfd6-200">Request time out</span></span>

### <a name="cause"></a><span data-ttu-id="4dfd6-201">Cause</span><span class="sxs-lookup"><span data-stu-id="4dfd6-201">Cause</span></span>

<span data-ttu-id="4dfd6-202">When a user request is received, Application Gateway applies the configured rules to the request and routes it to a back-end pool instance.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-202">When a user request is received, Application Gateway applies the configured rules to the request and routes it to a back-end pool instance.</span></span> <span data-ttu-id="4dfd6-203">It waits for a configurable interval of time for a response from the back-end instance.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-203">It waits for a configurable interval of time for a response from the back-end instance.</span></span> <span data-ttu-id="4dfd6-204">By default, this interval is **30 seconds**.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-204">By default, this interval is **30 seconds**.</span></span> <span data-ttu-id="4dfd6-205">If Application Gateway does not receive a response from back-end application in this interval, user request would see a 502 error.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-205">If Application Gateway does not receive a response from back-end application in this interval, user request would see a 502 error.</span></span>

### <a name="solution"></a><span data-ttu-id="4dfd6-206">Solution</span><span class="sxs-lookup"><span data-stu-id="4dfd6-206">Solution</span></span>

<span data-ttu-id="4dfd6-207">Application Gateway allows users to configure this setting via BackendHttpSetting, which can be then applied to different pools.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-207">Application Gateway allows users to configure this setting via BackendHttpSetting, which can be then applied to different pools.</span></span> <span data-ttu-id="4dfd6-208">Different back-end pools can have different BackendHttpSetting and hence different request time out configured.</span><span class="sxs-lookup"><span data-stu-id="4dfd6-208">Different back-end pools can have different BackendHttpSetting and hence different request time out configured.</span></span>

```powershell
    New-AzureRmApplicationGatewayBackendHttpSettings -Name 'Setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 60
```

## <a name="next-steps"></a><span data-ttu-id="4dfd6-209">Next steps</span><span class="sxs-lookup"><span data-stu-id="4dfd6-209">Next steps</span></span>

<span data-ttu-id="4dfd6-210">If the preceding steps do not resolve the issue, open a [support ticket](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="4dfd6-210">If the preceding steps do not resolve the issue, open a [support ticket](https://azure.microsoft.com/support/options/).</span></span>

