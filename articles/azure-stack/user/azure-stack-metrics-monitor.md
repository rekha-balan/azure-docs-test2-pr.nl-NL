---
title: Consume monitoring data from Azure Stack | Microsoft Docs
description: Learn about options for consuming monitoring data from Azure Stack.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/05/2018
ms.author: mabrigg
ms.openlocfilehash: 3d856f4fad845dfdd4d9a30fa176a4c0bfbc875b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966569"
---
# <a name="how-to-consume-monitoring-data-from-azure-stack"></a>How to consume monitoring data from Azure Stack

*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*

You can find monitoring data in a single place with the Azure Monitor pipeline, just like Azure Monitor in global Azure. But not all of the monitoring data found in global Azure is available in Azure Stack. In this article, you can find a summary of the various ways that you can programmatically ingest monitoring data from the service.
 
## <a name="options-for-data-consumption"></a>Options for data consumption

| Data type | Category | Supported services | Methods of access |
|-------------------------------------------------------------|----------|------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------|
| Azure Monitor platform-level metrics | Metrics | [Supported metrics with Azure Monitor on Azure Stack](azure-stack-metrics-supported.md) | REST API |
| Compute guest OS metrics (for example, Perf count) | Metrics | Windows and Linux Virtual Machines | Storage table or blob:<br>Windows or Linux Azure Diagnostics <br>Event Hub:<br>Windows Azure Diagnostics |
| Storage metrics | Metrics | Azure Storage | Storage table:<br>Storage Analytics |
| Activity log | Events | All Azure Services | REST API:<br>Azure Monitor Event API |
| Compute guest OS logs (for example,  IIS, ETW, syslogs) | Events | Windows and Linux Virtual Machines | Storage table or blob:<br>Windows or Linux Azure Diagnostics <br>Event Hub:<br>Windows Azure Diagnostics |
| Storage logs | Events | Azure Storage | Storage table:<br>Storage Analytics<br>`Vita: how about hybrid OMS/AppInsights, shall we mention?` |

## <a name="next-steps"></a>Next steps

Learn more about [Azure monitor on Azure Stack](azure-stack-metrics-azure-data.md).
