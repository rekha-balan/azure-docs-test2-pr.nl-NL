---
title: Manage Network Security Group flow logs with Azure Network Watcher | Microsoft Docs
description: This page explains how to manage Network Security Group flow logs in Azure Network Watcher
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: 01606cbf-d70b-40ad-bc1d-f03bb642e0af
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 580fc6e30e867cc77a08a53153fe5b801e02dbcc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551110"
---
# <a name="manage-network-security-group-flow-logs-in-the-azure-portal"></a><span data-ttu-id="77cff-103">Manage Network Security Group flow logs in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="77cff-103">Manage Network Security Group flow logs in the Azure portal</span></span>

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [CLI](network-watcher-nsg-flow-logging-cli.md)
> - [REST API](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="77cff-108">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span><span class="sxs-lookup"><span data-stu-id="77cff-108">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="77cff-109">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span><span class="sxs-lookup"><span data-stu-id="77cff-109">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="77cff-110">Before you begin</span><span class="sxs-lookup"><span data-stu-id="77cff-110">Before you begin</span></span>

<span data-ttu-id="77cff-111">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="77cff-111">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="77cff-112">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span><span class="sxs-lookup"><span data-stu-id="77cff-112">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="enable-flow-logs"></a><span data-ttu-id="77cff-113">Enable flow logs</span><span class="sxs-lookup"><span data-stu-id="77cff-113">Enable flow logs</span></span>

<span data-ttu-id="77cff-114">These steps take you through enabling Flow logs on a Network Security Group.</span><span class="sxs-lookup"><span data-stu-id="77cff-114">These steps take you through enabling Flow logs on a Network Security Group.</span></span>

### <a name="step-1"></a><span data-ttu-id="77cff-115">Step 1</span><span class="sxs-lookup"><span data-stu-id="77cff-115">Step 1</span></span>

<span data-ttu-id="77cff-116">Navigate to a Network Watcher instance and select **Flow logs**</span><span class="sxs-lookup"><span data-stu-id="77cff-116">Navigate to a Network Watcher instance and select **Flow logs**</span></span>

![flow logs overview][1]

### <a name="step-2"></a><span data-ttu-id="77cff-118">Step 2</span><span class="sxs-lookup"><span data-stu-id="77cff-118">Step 2</span></span>

<span data-ttu-id="77cff-119">Select a Network Security Group from the list by clicking it.</span><span class="sxs-lookup"><span data-stu-id="77cff-119">Select a Network Security Group from the list by clicking it.</span></span>

![flow logs overview][2]

### <a name="step-3"></a><span data-ttu-id="77cff-121">Step 3</span><span class="sxs-lookup"><span data-stu-id="77cff-121">Step 3</span></span> 

<span data-ttu-id="77cff-122">On the **Flow logs settings** blade, set the status to **On** and configure a storage account.</span><span class="sxs-lookup"><span data-stu-id="77cff-122">On the **Flow logs settings** blade, set the status to **On** and configure a storage account.</span></span>  <span data-ttu-id="77cff-123">When complete click **OK** and **Save**</span><span class="sxs-lookup"><span data-stu-id="77cff-123">When complete click **OK** and **Save**</span></span>

![flow logs overview][3]

## <a name="download-flow-logs"></a><span data-ttu-id="77cff-125">Download Flow logs</span><span class="sxs-lookup"><span data-stu-id="77cff-125">Download Flow logs</span></span>

<span data-ttu-id="77cff-126">Flow logs are saved in a storage account.</span><span class="sxs-lookup"><span data-stu-id="77cff-126">Flow logs are saved in a storage account.</span></span> <span data-ttu-id="77cff-127">To view your flow logs you need to download them.</span><span class="sxs-lookup"><span data-stu-id="77cff-127">To view your flow logs you need to download them.</span></span>

### <a name="step-1"></a><span data-ttu-id="77cff-128">Step 1</span><span class="sxs-lookup"><span data-stu-id="77cff-128">Step 1</span></span>

<span data-ttu-id="77cff-129">To download Flow logs, click **You can download flow logs from configured storage accounts**.</span><span class="sxs-lookup"><span data-stu-id="77cff-129">To download Flow logs, click **You can download flow logs from configured storage accounts**.</span></span>  <span data-ttu-id="77cff-130">This will take you to a storage account view where you can navigate to your log to download.</span><span class="sxs-lookup"><span data-stu-id="77cff-130">This will take you to a storage account view where you can navigate to your log to download.</span></span>

![flow logs settings][4]

### <a name="step-2"></a><span data-ttu-id="77cff-132">Step 2</span><span class="sxs-lookup"><span data-stu-id="77cff-132">Step 2</span></span>

<span data-ttu-id="77cff-133">Navigate to the correct storage account and then **Containers** > **insights-log-networksecuritygroupflowevent**</span><span class="sxs-lookup"><span data-stu-id="77cff-133">Navigate to the correct storage account and then **Containers** > **insights-log-networksecuritygroupflowevent**</span></span>

![flow logs settings][5]

### <a name="step-3"></a><span data-ttu-id="77cff-135">Step 3</span><span class="sxs-lookup"><span data-stu-id="77cff-135">Step 3</span></span>

<span data-ttu-id="77cff-136">Drill down to the location of the flow log, select the flow log and click **Download**</span><span class="sxs-lookup"><span data-stu-id="77cff-136">Drill down to the location of the flow log, select the flow log and click **Download**</span></span>

![flow logs settings][6]

<span data-ttu-id="77cff-138">For information about the structure of the log visit [Network Security Group flow log Overview](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="77cff-138">For information about the structure of the log visit [Network Security Group flow log Overview](network-watcher-nsg-flow-logging-overview.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="77cff-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="77cff-139">Next steps</span></span>

<span data-ttu-id="77cff-140">Learn how to [Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="77cff-140">Learn how to [Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<!-- Image references -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-nsg-flow-logging-portal/figure1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-nsg-flow-logging-portal/figure2.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-nsg-flow-logging-portal/figure3.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-nsg-flow-logging-portal/figure4.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-nsg-flow-logging-portal/figure5.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-nsg-flow-logging-portal/figure6.png






