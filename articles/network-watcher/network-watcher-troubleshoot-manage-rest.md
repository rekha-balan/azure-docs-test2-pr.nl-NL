---
title: Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher - REST | Microsoft Docs
description: This page explains how to troubleshoot Virtual Network Gateways and Connections with Azure Network Watcher using REST
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: e4d5f195-b839-4394-94ef-a04192766e55
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 7c2df4c1a7e1ff3cae19a160ffe6f6562afd3a0c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552535"
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher"></a><span data-ttu-id="a01f2-103">Troubleshoot Virtual Network gateway and Connections using Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="a01f2-103">Troubleshoot Virtual Network gateway and Connections using Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [CLI](network-watcher-troubleshoot-manage-cli.md)
> - [REST API](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="a01f2-107">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span><span class="sxs-lookup"><span data-stu-id="a01f2-107">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span></span> <span data-ttu-id="a01f2-108">One of these capabilities is resource troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="a01f2-108">One of these capabilities is resource troubleshooting.</span></span>  <span data-ttu-id="a01f2-109">Resource troubleshooting can be called by PowerShell, CLI, or REST API.</span><span class="sxs-lookup"><span data-stu-id="a01f2-109">Resource troubleshooting can be called by PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="a01f2-110">When called, Network Watcher inspects the health of a Virtual Network gateway or a Connection and returns its findings.</span><span class="sxs-lookup"><span data-stu-id="a01f2-110">When called, Network Watcher inspects the health of a Virtual Network gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="a01f2-111">This article takes you through the different management tasks that are currently available for resource troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="a01f2-111">This article takes you through the different management tasks that are currently available for resource troubleshooting.</span></span>

- [<span data-ttu-id="a01f2-112">**Troubleshoot a Virtual Network gateway**</span><span class="sxs-lookup"><span data-stu-id="a01f2-112">**Troubleshoot a Virtual Network gateway**</span></span>](#troubleshoot-a-virtual-network-gateway)
- [<span data-ttu-id="a01f2-113">**Troubleshoot a Connection**</span><span class="sxs-lookup"><span data-stu-id="a01f2-113">**Troubleshoot a Connection**</span></span>](#troubleshoot-connections)

## <a name="before-you-begin"></a><span data-ttu-id="a01f2-114">Before you begin</span><span class="sxs-lookup"><span data-stu-id="a01f2-114">Before you begin</span></span>

<span data-ttu-id="a01f2-115">ARMclient is used to call the REST API using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a01f2-115">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="a01f2-116">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="a01f2-116">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="a01f2-117">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="a01f2-117">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="overview"></a><span data-ttu-id="a01f2-118">Overview</span><span class="sxs-lookup"><span data-stu-id="a01f2-118">Overview</span></span>

<span data-ttu-id="a01f2-119">Network Watcher troubleshooting provides the ability troubleshoot issues that arise with Virtual Network gateways and Connections.</span><span class="sxs-lookup"><span data-stu-id="a01f2-119">Network Watcher troubleshooting provides the ability troubleshoot issues that arise with Virtual Network gateways and Connections.</span></span> <span data-ttu-id="a01f2-120">When a request is made to the resource troubleshooting, logs are querying and inspected.</span><span class="sxs-lookup"><span data-stu-id="a01f2-120">When a request is made to the resource troubleshooting, logs are querying and inspected.</span></span> <span data-ttu-id="a01f2-121">When inspection is complete, the results are returned.</span><span class="sxs-lookup"><span data-stu-id="a01f2-121">When inspection is complete, the results are returned.</span></span> <span data-ttu-id="a01f2-122">The troubleshoot API requests are long running requests, which could take multiple minutes to return a result.</span><span class="sxs-lookup"><span data-stu-id="a01f2-122">The troubleshoot API requests are long running requests, which could take multiple minutes to return a result.</span></span> <span data-ttu-id="a01f2-123">Logs are stored in a container on a storage account.</span><span class="sxs-lookup"><span data-stu-id="a01f2-123">Logs are stored in a container on a storage account.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="a01f2-124">Log in with ARMClient</span><span class="sxs-lookup"><span data-stu-id="a01f2-124">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="troubleshoot-a-virtual-network-gateway"></a><span data-ttu-id="a01f2-125">Troubleshoot a Virtual Network gateway</span><span class="sxs-lookup"><span data-stu-id="a01f2-125">Troubleshoot a Virtual Network gateway</span></span>


### <a name="post-the-troubleshoot-request"></a><span data-ttu-id="a01f2-126">POST the troubleshoot request</span><span class="sxs-lookup"><span data-stu-id="a01f2-126">POST the troubleshoot request</span></span>

<span data-ttu-id="a01f2-127">The following example queries the status of a Virtual Network gateway.</span><span class="sxs-lookup"><span data-stu-id="a01f2-127">The following example queries the status of a Virtual Network gateway.</span></span>

```powershell

$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "ContosoRG"
$NWresourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$vnetGatewayName = "ContosoVNETGateway"
$storageAccountName = "contososa"
$containerName = "gwlogs"
$requestBody = @"
{
'TargetResourceId': '/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/virtualNetworkGateways/${vnetGatewayName}',
'Properties': {
'StorageId': '/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Storage/storageAccounts/${storageAccountName}',
'StoragePath': 'https://${storageAccountName}.blob.core.windows.net/${containerName}'
}
}
"@

}
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/troubleshoot?api-version=2016-03-30 "
```

<span data-ttu-id="a01f2-128">Since this operation is long running, the URI for querying the operation and the URI for the result is returned in the response header as shown in the following response:</span><span class="sxs-lookup"><span data-stu-id="a01f2-128">Since this operation is long running, the URI for querying the operation and the URI for the result is returned in the response header as shown in the following response:</span></span>

<span data-ttu-id="a01f2-129">**Important Values**</span><span class="sxs-lookup"><span data-stu-id="a01f2-129">**Important Values**</span></span>

* <span data-ttu-id="a01f2-130">**Azure-AsyncOperation** - This property contains the URI to query the Async troubleshoot operation</span><span class="sxs-lookup"><span data-stu-id="a01f2-130">**Azure-AsyncOperation** - This property contains the URI to query the Async troubleshoot operation</span></span>
* <span data-ttu-id="a01f2-131">**Location** - This property contains the URI where the results are when the operation is complete</span><span class="sxs-lookup"><span data-stu-id="a01f2-131">**Location** - This property contains the URI where the results are when the operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 8a1167b7-6768-4ac1-85dc-703c9c9b9247
Azure-AsyncOperation: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4364d88a-bd08-422c-a716-dbb0cdc99f7b
x-ms-routing-request-id: NORTHCENTRALUS:20170112T183202Z:4364d88a-bd08-422c-a716-dbb0cdc99f7b
Date: Thu, 12 Jan 2017 18:32:01 GMT

null
```

### <a name="query-the-async-operation-for-completion"></a><span data-ttu-id="a01f2-132">Query the async operation for completion</span><span class="sxs-lookup"><span data-stu-id="a01f2-132">Query the async operation for completion</span></span>

<span data-ttu-id="a01f2-133">Use the operations URI to query for the progress of the operation as seen in the following example:</span><span class="sxs-lookup"><span data-stu-id="a01f2-133">Use the operations URI to query for the progress of the operation as seen in the following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="a01f2-134">While the operation is in progress, the response shows **InProgress** as seen in the following example:</span><span class="sxs-lookup"><span data-stu-id="a01f2-134">While the operation is in progress, the response shows **InProgress** as seen in the following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="a01f2-135">When the operation is complete the status changes to **Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="a01f2-135">When the operation is complete the status changes to **Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

### <a name="retrieve-the-results"></a><span data-ttu-id="a01f2-136">Retrieve the results</span><span class="sxs-lookup"><span data-stu-id="a01f2-136">Retrieve the results</span></span>

<span data-ttu-id="a01f2-137">Once the status returned is **Succeeded**, call a GET Method on the operationResult URI to retrieve the results.</span><span class="sxs-lookup"><span data-stu-id="a01f2-137">Once the status returned is **Succeeded**, call a GET Method on the operationResult URI to retrieve the results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="a01f2-138">The following responses are examples of a typical degraded response returned when querying the results of troubleshooting a gateway.</span><span class="sxs-lookup"><span data-stu-id="a01f2-138">The following responses are examples of a typical degraded response returned when querying the results of troubleshooting a gateway.</span></span> <span data-ttu-id="a01f2-139">See [Understanding the results](#understanding-the-results) to get clarification on what the properties in the response mean.</span><span class="sxs-lookup"><span data-stu-id="a01f2-139">See [Understanding the results](#understanding-the-results) to get clarification on what the properties in the response mean.</span></span>

```json
{
  "startTime": "2017-01-12T10:31:41.562646-08:00",
  "endTime": "2017-01-12T18:31:48.677Z",
  "code": "Degraded",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time the gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This is a transient state while the Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If the condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting the VPN Gateway"
        },
        {
          "actionText": "If your VPN gateway isn't up and running by the expected resolution time, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    },
    {
      "id": "NoFault",
      "summary": "This VPN gateway is running normally",
      "detail": "There aren't any known Azure platform problems affecting this VPN Connection",
      "recommendedActions": [
        {
          "actionText": "If you are still experience problems with the VPN gateway, please try resetting the VPN gateway.",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting VPN gateway"
        },
        {
          "actionText": "If you are experiencing problems you believe are caused by Azure, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    }
  ]
}
```


## <a name="troubleshoot-connections"></a><span data-ttu-id="a01f2-140">Troubleshoot Connections</span><span class="sxs-lookup"><span data-stu-id="a01f2-140">Troubleshoot Connections</span></span>

<span data-ttu-id="a01f2-141">The following example queries the status of a Connection.</span><span class="sxs-lookup"><span data-stu-id="a01f2-141">The following example queries the status of a Connection.</span></span>

```powershell

$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "ContosoRG"
$NWresourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$connectionName = "VNET2toVNET1Connection"
$storageAccountName = "contososa"
$containerName = "gwlogs"
$requestBody = @{
"TargetResourceId": "/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/connections/${connectionName}",
"Properties": {
"StorageId": "/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Storage/storageAccounts/${storageAccountName}",
"StoragePath": "https://${storageAccountName}.blob.core.windows.net/${containerName}"
}

}
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/troubleshoot?api-version=2016-03-30 "
```

> [!NOTE]
> The troubleshoot operation cannot be run in parallel on a Connection and its corresponding gateways. The operation must complete prior to running it on the previous resource.

<span data-ttu-id="a01f2-144">Since this is a long running transaction, in the response header, the URI for querying the operation and the URI for the result is returned as shown in the following response:</span><span class="sxs-lookup"><span data-stu-id="a01f2-144">Since this is a long running transaction, in the response header, the URI for querying the operation and the URI for the result is returned as shown in the following response:</span></span>

<span data-ttu-id="a01f2-145">**Important Values**</span><span class="sxs-lookup"><span data-stu-id="a01f2-145">**Important Values**</span></span>

* <span data-ttu-id="a01f2-146">**Azure-AsyncOperation** - This property contains the URI to query the Async troubleshoot operation</span><span class="sxs-lookup"><span data-stu-id="a01f2-146">**Azure-AsyncOperation** - This property contains the URI to query the Async troubleshoot operation</span></span>
* <span data-ttu-id="a01f2-147">**Location** - This property contains the URI where the results are when the operation is complete</span><span class="sxs-lookup"><span data-stu-id="a01f2-147">**Location** - This property contains the URI where the results are when the operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 8a1167b7-6768-4ac1-85dc-703c9c9b9247
Azure-AsyncOperation: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4364d88a-bd08-422c-a716-dbb0cdc99f7b
x-ms-routing-request-id: NORTHCENTRALUS:20170112T183202Z:4364d88a-bd08-422c-a716-dbb0cdc99f7b
Date: Thu, 12 Jan 2017 18:32:01 GMT

null
```

### <a name="query-the-async-operation-for-completion"></a><span data-ttu-id="a01f2-148">Query the async operation for completion</span><span class="sxs-lookup"><span data-stu-id="a01f2-148">Query the async operation for completion</span></span>

<span data-ttu-id="a01f2-149">Use the operations URI to query for the progress of the operation as seen in the following example:</span><span class="sxs-lookup"><span data-stu-id="a01f2-149">Use the operations URI to query for the progress of the operation as seen in the following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="a01f2-150">While the operation is in progress, the response shows **InProgress** as seen in the following example:</span><span class="sxs-lookup"><span data-stu-id="a01f2-150">While the operation is in progress, the response shows **InProgress** as seen in the following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="a01f2-151">When the operation is complete, the status changes to **Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="a01f2-151">When the operation is complete, the status changes to **Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

<span data-ttu-id="a01f2-152">The following responses are examples of a typical response returned when querying the results of troubleshooting a Connection.</span><span class="sxs-lookup"><span data-stu-id="a01f2-152">The following responses are examples of a typical response returned when querying the results of troubleshooting a Connection.</span></span>

### <a name="retrieve-the-results"></a><span data-ttu-id="a01f2-153">Retrieve the results</span><span class="sxs-lookup"><span data-stu-id="a01f2-153">Retrieve the results</span></span>

<span data-ttu-id="a01f2-154">Once the status returned is **Succeeded**, call a GET Method on the operationResult URI to retrieve the results.</span><span class="sxs-lookup"><span data-stu-id="a01f2-154">Once the status returned is **Succeeded**, call a GET Method on the operationResult URI to retrieve the results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="a01f2-155">The following responses are examples of a typical response returned when querying the results of troubleshooting a Connection.</span><span class="sxs-lookup"><span data-stu-id="a01f2-155">The following responses are examples of a typical response returned when querying the results of troubleshooting a Connection.</span></span>

```json
{
  "startTime": "2017-01-12T14:09:19.1215346-08:00",
  "endTime": "2017-01-12T22:09:23.747Z",
  "code": "UnHealthy",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time the gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This 
is a transient state while the Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If the condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting the VPN gateway"
        },
        {
          "actionText": "If your VPN Connection isn't up and running by the expected resolution time, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    },
    {
      "id": "NoFault",
      "summary": "This VPN Connection is running normally",
      "detail": "There aren't any known Azure platform problems affecting this VPN Connection",
      "recommendedActions": [
        {
          "actionText": "If you are still experience problems with the VPN gateway, please try resetting the VPN gateway.",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting VPN gateway"
        },
        {
          "actionText": "If you are experiencing problems you believe are caused by Azure, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    }
  ]
}
```

## <a name="understanding-the-results"></a><span data-ttu-id="a01f2-156">Understanding the results</span><span class="sxs-lookup"><span data-stu-id="a01f2-156">Understanding the results</span></span>

<span data-ttu-id="a01f2-157">The action text provides general guidance on how to resolve the issue.</span><span class="sxs-lookup"><span data-stu-id="a01f2-157">The action text provides general guidance on how to resolve the issue.</span></span> <span data-ttu-id="a01f2-158">If an action can be taken for the issue, a link is provided with additional guidance.</span><span class="sxs-lookup"><span data-stu-id="a01f2-158">If an action can be taken for the issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="a01f2-159">In the case where there is no additional guidance, the response provides the url to open a support case.</span><span class="sxs-lookup"><span data-stu-id="a01f2-159">In the case where there is no additional guidance, the response provides the url to open a support case.</span></span>  <span data-ttu-id="a01f2-160">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="a01f2-160">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="a01f2-161">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="a01f2-161">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="a01f2-162">Another tool that can be used is Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="a01f2-162">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="a01f2-163">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="a01f2-163">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="a01f2-164">Next steps</span><span class="sxs-lookup"><span data-stu-id="a01f2-164">Next steps</span></span>

<span data-ttu-id="a01f2-165">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span><span class="sxs-lookup"><span data-stu-id="a01f2-165">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span></span>
