---
title: Resolve endpoint protection health alerts in Azure Security Center| Microsoft Docs
description: This document shows you how to implement the Azure Security Center recommendation **Resolve Endpoint Protection health alerts**.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: ''
ms.assetid: 4050f453-98fc-4314-8438-d476469757fb
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/01/2016
ms.author: terrylan
ms.openlocfilehash: 02b11701409ba59f95f65535a26edc626fff6443
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44663023"
---
# <a name="resolve-endpoint-protection-health-alerts-in-azure-security-center"></a>Resolve endpoint protection health alerts in Azure Security Center
Azure Security Center will recommend that you resolve detected endpoint protection health alerts.  Security Center enables you to see which virtual machines (VMs) have endpoint protection failures and how many failures.

> [!NOTE]
> This document introduces the service by using an example deployment. This is not a step-by-step guide.
> 
> 

## <a name="implement-the-recommendation"></a>Implement the recommendation
1. In the **Recommendations blade**, select **Resolve Endpoint Protection health alerts**.
   ![Resolve endpoint protection health alerts][1]
2. This opens the blade **Endpoint Protection failure** which lists VMs with failures and the number of failures for each VM. Select a VM from the list.
   ![Endpoint protection failure][2]
3. A **Failures List** blade opens for the selected VM, displaying a list of failures. Select a failure from the list to learn more. This opens a blade with information about the selected failure.
   ![Failures list][3]
   ![Failure event][4]

## <a name="see-also"></a>See also
To learn more about Security Center, see the following:

* [Setting security policies in Azure Security Center](security-center-policies.md)--Learn how to configure security policies for your Azure subscriptions and resource groups.
* [Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.
* [Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how to monitor the health of your Azure resources.
* [Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how to manage and respond to security alerts.
* [Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.
* [Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.
* [Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get the latest Azure security news and information.

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-resolve-endpoint-protection/resolve-endpoint-protection.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-resolve-endpoint-protection/endpoint-protection-failure.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-resolve-endpoint-protection/failure-list.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-resolve-endpoint-protection/failure-event.png




