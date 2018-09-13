---
title: Add a web application firewall in Azure Security Center | Microsoft Docs
description: This document shows you how to implement the Azure Security Center recommendations **Add a web application firewall** and **Finalize application protection**.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: ''
ms.assetid: 8f56139a-4466-48ac-90fb-86d002cf8242
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/01/2016
ms.author: terrylan
ms.openlocfilehash: e2db22558807751296f2762b2fc9ab103823380b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562920"
---
# <a name="add-a-web-application-firewall-in-azure-security-center"></a>Add a web application firewall in Azure Security Center
Azure Security Center may recommend that you add a web application firewall (WAF) from a Microsoft partner to secure your web applications. This document walks you through an example of how to apply this recommendation.

A WAF recommendation is shown for any public facing IP (either Instance Level IP or Load Balanced IP) that has an associated network security group with open inbound web ports (80,443).

Security Center recommends that you provision a WAF to help defend against attacks targeting your web applications on virtual machines and on App Service Environment. An App Service Environment (ASE) is a [Premium](https://azure.microsoft.com/pricing/details/app-service/) service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps. To learn more about ASE, see the [App Service Environment Documentation](../app-service/app-service-app-service-environments-readme.md).

> [!NOTE]
> This document introduces the service by using an example deployment.  This document is not a step-by-step guide.
>
>

## <a name="implement-the-recommendation"></a>Implement the recommendation
1. In the **Recommendations** blade, select **Secure web application using web application firewall**.
   ![Secure web Application][1]
2. In the **Secure your web applications using web application firewall** blade, select a web application. The **Add a Web Application Firewall** blade opens.
   ![Add a web application firewall][2]
3. You can choose to use an existing web application firewall if available or you can create a new one. In this example, there are no existing WAFs available so we create a WAF.
4. To create a WAF, select a solution from the list of integrated partners. In this example, we select **Barracuda Web Application Firewall**.
5. The **Barracuda Web Application Firewall** blade opens providing you information about the partner solution. Select **Create** in the information blade.
   ![Firewall information blade][3]
6. The **New Web Application Firewall** blade opens, where you can perform **VM Configuration** steps and provide **WAF Information**. Select **VM Configuration**.
7. In the **VM Configuration** blade, you enter information required to spin up the virtual machine that runs the WAF.
   ![VM configuration][4]
8. Return to the **New Web Application Firewall** blade and select **WAF Information**. In the **WAF Information** blade, you configure the WAF itself. Step 7 allows you to configure the virtual machine on which the WAF runs and step 8 enables you to provision the WAF itself.

## <a name="finalize-application-protection"></a>Finalize application protection
1. Return to the **Recommendations** blade. A new entry was generated after you created the WAF, called **Finalize application protection**. This entry lets you know that you need to complete the process of actually wiring up the WAF within the Azure Virtual Network so that it can protect the application.
   ![Finalize application protection][5]
2. Select **Finalize application protection**. A new blade opens. You can see that there is a web application that needs to have its traffic rerouted.
3. Select the web application. A blade opens that gives you steps for finalizing the web application firewall setup. Complete the steps, and then select **Restrict traffic**. Security Center then does the wiring-up for you.
   ![Restrict traffic][6]

> [!NOTE]
> You can protect multiple web applications in Security Center by adding these applications to your existing WAF deployments.
>
>

The logs from that WAF are now fully integrated. Security Center can start automatically gathering and analyzing the logs so that it can surface important security alerts to you.

## <a name="see-also"></a>See also
This document showed you how to implement the Security Center recommendation "Add a web application." To learn more about configuring a web application firewall, see the following:

* [Configuring a Web Application Firewall (WAF) for App Service Environment](../app-service-web/app-service-app-service-environment-web-application-firewall.md)

To learn more about Security Center, see the following:

* [Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.
* [Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.
* [Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.
* [Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.
* [Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.
* [Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-add-web-application-firewall/secure-web-application.png
[2]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-add-web-application-firewall/add-a-waf.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-add-web-application-firewall/info-blade.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-add-web-application-firewall/select-vm-config.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-add-web-application-firewall/finalize-waf.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-add-web-application-firewall/restrict-traffic.png






