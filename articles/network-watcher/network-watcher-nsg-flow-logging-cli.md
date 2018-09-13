---
title: Manage Network Security Group Flow logs with Azure Network Watcher - Azure CLI | Microsoft Docs
description: This page explains how to manage Network Security Group Flow logs in Azure Network Watcher with Azure CLI
services: network-watcher
documentationcenter: na
author: jimdial
manager: timlt
editor: ''
ms.assetid: 2dfc3112-8294-4357-b2f8-f81840da67d3
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: jdial
ms.openlocfilehash: 43552ae2d7601a63156ac74104b85a90326ff473
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44811875"
---
# <a name="configuring-network-security-group-flow-logs-with-azure-cli"></a><span data-ttu-id="3bfd6-103">Configuring Network Security Group Flow logs with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3bfd6-103">Configuring Network Security Group Flow logs with Azure CLI</span></span>

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [Azure CLI](network-watcher-nsg-flow-logging-cli.md)
> - [REST API](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="3bfd6-108">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span><span class="sxs-lookup"><span data-stu-id="3bfd6-108">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="3bfd6-109">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span><span class="sxs-lookup"><span data-stu-id="3bfd6-109">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

<span data-ttu-id="3bfd6-110">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span><span class="sxs-lookup"><span data-stu-id="3bfd6-110">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="3bfd6-111">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="3bfd6-111">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="3bfd6-112">Register Insights provider</span><span class="sxs-lookup"><span data-stu-id="3bfd6-112">Register Insights provider</span></span>

<span data-ttu-id="3bfd6-113">In order for flow logging to work successfully, the **Microsoft.Insights** provider must be registered.</span><span class="sxs-lookup"><span data-stu-id="3bfd6-113">In order for flow logging to work successfully, the **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="3bfd6-114">If you are not sure if the **Microsoft.Insights** provider is registered, run the following script.</span><span class="sxs-lookup"><span data-stu-id="3bfd6-114">If you are not sure if the **Microsoft.Insights** provider is registered, run the following script.</span></span>

```azurecli
az provider register --namespace Microsoft.Insights
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="3bfd6-115">Enable Network Security Group Flow logs</span><span class="sxs-lookup"><span data-stu-id="3bfd6-115">Enable Network Security Group Flow logs</span></span>

<span data-ttu-id="3bfd6-116">The command to enable flow logs is shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="3bfd6-116">The command to enable flow logs is shown in the following example:</span></span>

```azurecli
az network watcher flow-log configure --resource-group resourceGroupName --enabled true --nsg nsgName --storage-account storageAccountName
```

<span data-ttu-id="3bfd6-117">The storage account that you specify cannot have network rules configured for it that restrict network access to only Microsoft services or specific virtual networks.</span><span class="sxs-lookup"><span data-stu-id="3bfd6-117">The storage account that you specify cannot have network rules configured for it that restrict network access to only Microsoft services or specific virtual networks.</span></span> <span data-ttu-id="3bfd6-118">The storage account can be in the same, or a different Azure subscription, than the NSG that you enable the flow log for.</span><span class="sxs-lookup"><span data-stu-id="3bfd6-118">The storage account can be in the same, or a different Azure subscription, than the NSG that you enable the flow log for.</span></span> <span data-ttu-id="3bfd6-119">If you use different subscriptions, they must both be associated to the same Azure Active Directory tenant.</span><span class="sxs-lookup"><span data-stu-id="3bfd6-119">If you use different subscriptions, they must both be associated to the same Azure Active Directory tenant.</span></span> <span data-ttu-id="3bfd6-120">The account you use for each subscription must have the [necessary permissions](required-rbac-permissions.md).</span><span class="sxs-lookup"><span data-stu-id="3bfd6-120">The account you use for each subscription must have the [necessary permissions](required-rbac-permissions.md).</span></span> 

<span data-ttu-id="3bfd6-121">If the storage account is in a different resource group, or subscription, than the network security group, specify the full ID of the storage account, rather than its name.</span><span class="sxs-lookup"><span data-stu-id="3bfd6-121">If the storage account is in a different resource group, or subscription, than the network security group, specify the full ID of the storage account, rather than its name.</span></span> <span data-ttu-id="3bfd6-122">For example, if the storage account is in a resource group named *RG-Storage*, rather than specifying *storageAccountName* in the previous command, you'd specify */subscriptions/{SubscriptionID}/resourceGroups/RG-Storage/providers/Microsoft.Storage/storageAccounts/storageAccountName*.</span><span class="sxs-lookup"><span data-stu-id="3bfd6-122">For example, if the storage account is in a resource group named *RG-Storage*, rather than specifying *storageAccountName* in the previous command, you'd specify */subscriptions/{SubscriptionID}/resourceGroups/RG-Storage/providers/Microsoft.Storage/storageAccounts/storageAccountName*.</span></span>

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="3bfd6-123">Disable Network Security Group Flow logs</span><span class="sxs-lookup"><span data-stu-id="3bfd6-123">Disable Network Security Group Flow logs</span></span>

<span data-ttu-id="3bfd6-124">Use the following example to disable flow logs:</span><span class="sxs-lookup"><span data-stu-id="3bfd6-124">Use the following example to disable flow logs:</span></span>

```azurecli
az network watcher flow-log configure --resource-group resourceGroupName --enabled false --nsg nsgName
```

## <a name="download-a-flow-log"></a><span data-ttu-id="3bfd6-125">Download a Flow log</span><span class="sxs-lookup"><span data-stu-id="3bfd6-125">Download a Flow log</span></span>

<span data-ttu-id="3bfd6-126">The storage location of a flow log is defined at creation.</span><span class="sxs-lookup"><span data-stu-id="3bfd6-126">The storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="3bfd6-127">A convenient tool to access these flow logs saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="3bfd6-127">A convenient tool to access these flow logs saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="3bfd6-128">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span><span class="sxs-lookup"><span data-stu-id="3bfd6-128">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId=/SUBSCRIPTIONS/{subscriptionID}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/{nsgName}/y={year}/m={month}/d={day}/h={hour}/m=00/macAddress={macAddress}/PT1H.json
```

<span data-ttu-id="3bfd6-129">For information about the structure of the log visit [Network Security Group Flow log Overview](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="3bfd6-129">For information about the structure of the log visit [Network Security Group Flow log Overview](network-watcher-nsg-flow-logging-overview.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="3bfd6-130">Next Steps</span><span class="sxs-lookup"><span data-stu-id="3bfd6-130">Next Steps</span></span>

<span data-ttu-id="3bfd6-131">Learn how to [Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="3bfd6-131">Learn how to [Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="3bfd6-132">Learn how to [Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="3bfd6-132">Learn how to [Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
