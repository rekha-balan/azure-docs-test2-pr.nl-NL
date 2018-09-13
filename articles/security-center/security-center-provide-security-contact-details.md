---
title: Provide security contact details in Azure Security Center | Microsoft Docs
description: This document shows you how to provide security contact details in Azure Security Center.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: ''
ms.assetid: 26b5dcb4-ce3f-4f22-8d56-d2bf743cfc90
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 624fbda7bd8b83eb53e2147eaea2c51326d36cff
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554592"
---
# <a name="provide-security-contact-details-in-azure-security-center"></a>Provide security contact details in Azure Security Center
Azure Security Center will recommend that you provide security contact details for your Azure subscription if you haven’t already. This information will be used by Microsoft to contact you if the Microsoft Security Response Center (MSRC) discovers that your customer data has been accessed by an unlawful or unauthorized party. MSRC performs select security monitoring of the Azure network and infrastructure and receives threat intelligence and abuse complaints from third parties.

An email notification is sent on the first daily occurrence of an alert and only for high severity alerts. Email preferences can only be configured for subscription policies. Resource groups within a subscription will inherit these settings.

> [!NOTE]
> This document introduces the service by using an example deployment.  This is not a step-by-step guide.
>
>

## <a name="implement-the-recommendation"></a>Implement the recommendation
1. In the **Recommendations** blade, select **Provide security contact details**.
   ![Provide security contact][1]
2. This opens the blade **Provide security contact details**. Select the Azure subscription to provide contact information on.
   ![Provide security contact details][2]
3. A second **Provide security contact details** blade opens.

   * Enter the security contact email address or addresses separated by commas. There is not a limit to the number of email addresses that you can enter.
   * Enter one security contact international phone number.
   * To receive emails about high severity alerts, turn on the option **Send me emails about alerts**.
   * In the future, you will have the option to send email notifications to subscription owners. This option is currently grayed out.
   * Select **OK** to apply the security contact information to your subscription.

## <a name="see-also"></a>See also
To learn more about Security Center, see the following:

* [Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.
* [Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.
* [Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.
* [Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.
* [Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.
* [Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.
* [Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-provide-security-contacts/provide-contacts.png
[2]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-provide-security-contacts/provide-contact-details.png


