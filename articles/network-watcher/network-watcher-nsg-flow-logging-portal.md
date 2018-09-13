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
# <a name="manage-network-security-group-flow-logs-in-the-azure-portal"></a>Manage Network Security Group flow logs in the Azure portal

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [CLI](network-watcher-nsg-flow-logging-cli.md)
> - [REST API](network-watcher-nsg-flow-logging-rest.md)

Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group. These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.

## <a name="before-you-begin"></a>Before you begin

This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher. The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.

## <a name="enable-flow-logs"></a>Enable flow logs

These steps take you through enabling Flow logs on a Network Security Group.

### <a name="step-1"></a>Step 1

Navigate to a Network Watcher instance and select **Flow logs**

![flow logs overview][1]

### <a name="step-2"></a>Step 2

Select a Network Security Group from the list by clicking it.

![flow logs overview][2]

### <a name="step-3"></a>Step 3 

On the **Flow logs settings** blade, set the status to **On** and configure a storage account.  When complete click **OK** and **Save**

![flow logs overview][3]

## <a name="download-flow-logs"></a>Download Flow logs

Flow logs are saved in a storage account. To view your flow logs you need to download them.

### <a name="step-1"></a>Step 1

To download Flow logs, click **You can download flow logs from configured storage accounts**.  This will take you to a storage account view where you can navigate to your log to download.

![flow logs settings][4]

### <a name="step-2"></a>Step 2

Navigate to the correct storage account and then **Containers** > **insights-log-networksecuritygroupflowevent**

![flow logs settings][5]

### <a name="step-3"></a>Step 3

Drill down to the location of the flow log, select the flow log and click **Download**

![flow logs settings][6]

For information about the structure of the log visit [Network Security Group flow log Overview](network-watcher-nsg-flow-logging-overview.md)

## <a name="next-steps"></a>Next steps

Learn how to [Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)

<!-- Image references -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-nsg-flow-logging-portal/figure1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-nsg-flow-logging-portal/figure2.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-nsg-flow-logging-portal/figure3.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-nsg-flow-logging-portal/figure4.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-nsg-flow-logging-portal/figure5.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-nsg-flow-logging-portal/figure6.png






