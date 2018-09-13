---
title: Managing partner solutions in Azure Security Center | Microsoft Docs
description: This document walks you through how Azure Security Center lets you monitor at a glance the health status of your partner solutions integrated with your Azure subscription.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: ''
ms.assetid: 70c076ef-3ad4-4000-a0c1-0ac0c9796ff1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: 74b495e0365823d839ce47bd390601f930cca240
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549269"
---
# <a name="monitoring-partner-solutions-with-azure-security-center"></a>Monitoring partner solutions with Azure Security Center
This document walks you through how to monitor the health status of your partner solutions in Azure Security Center.

> [!NOTE]
> This document introduces the service by using an example deployment. This is not a step-by-step guide.
>
>

## <a name="monitoring-partner-solutions"></a>Monitoring partner solutions
The **Partner solutions** tile on the **Security Center** blade lets you monitor at a glance the health status of your partner solutions integrated with your Azure subscription.

![Partner solutions tile][1]

The **Partner solutions** tile displays the number of partner solutions and a status summary for those solutions.

The **STATUS** of a partner solution can be:

* Protected (green) - there is no health issue.
* Unhealthy (red) - there is a health issue that requires immediate attention.
* Stopped reporting (orange) - the solution has stopped reporting its health.
* Unknown protection status (orange) - the health of the solution is unknown at this time due to a failed process of adding a new resource to the existing solution.
* Not reported (gray) - the solution has not reported anything yet, a solution's status may be unreported if it has just been connected and is still deploying.

If there are no solutions integrated with your subscription the tile will state that there are no solutions. Selecting the **Partner solutions** tile will enable you to open the **Recommendations** blade to deploy partner security solutions.

![No partner solutions][2]

To view the health of your partner solutions:

1. Select the **Partner solutions** tile. A blade opens displaying a list of your partner solutions connected to Security Center.

   ![Partner solutions][3]
2. Select a partner solution. In this example, lets select the **F5-WAF2** solution.  A blade opens showing you the status of the partner solution and the solution's associated resources. Select **Solution console** to open the partner management experience for this solution.

   ![Partner solution detail][4]
3. Go back to the **F5-WAF2** blade and select **Link app**. The **Link Applications** blade opens. Here you can connect resources to the partner solution.

   ![Link resources to partner solution][5]

## <a name="see-also"></a>See also
In this document, you were introduced to the **Partner Solutions** tile in Security Center. To learn more about Security Center, see the following:

* [Setting security policies in Azure Security Center](security-center-policies.md) — Learn how to configure security policies for your Azure subscriptions and resource groups.
* [Managing security recommendations in Azure Security Center](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.
* [Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how to monitor the health of your Azure resources.
* [Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts.
* [Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.
* [Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Get the latest Azure security news and information.

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-partner-solutions/partner-solutions-tile.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-partner-solutions/no-partner-solutions-to-display.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-partner-solutions/partner-solutions.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-partner-solutions/partner-solutions-detail.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-partner-solutions/link-applications.png





