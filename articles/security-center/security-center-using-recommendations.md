---
title: Use Azure Security Center recommendations to enhance security | Microsoft Docs
description: " Learn how to use security policies and recommendations in Azure Security Center to help mitigate a security attack. "
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: ''
ms.assetid: ''
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: terrylan
ms.openlocfilehash: abeaab18cb33c065a6e85795596257b81c3b0f52
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671859"
---
# <a name="use-azure-security-center-recommendations-to-enhance-security"></a>Use Azure Security Center recommendations to enhance security
You can reduce the chances of a significant security event by configuring a security policy and then implementing the recommendations provided by Azure Security Center. This article shows you how to use security policies and recommendations in Security Center to help mitigate a security attack.

> [!NOTE]
> This article builds on the roles and concepts introduced in the Security Center [planning and operations guide](security-center-planning-and-operations-guide.md). It’s a good idea to review the planning guide before continuing.
>
>

## <a name="managing-security-recommendations"></a>Managing security recommendations
A security policy defines the set of controls that are recommended for resources within the specified subscription or resource group. In Security Center, you define policies according to your company's security requirements. To learn more, see [Set security policies in Security Center](security-center-policies.md).

Security policies for resource groups are inherited from the subscription level.

![Security policy inheritance][1]

If you need custom policies in specific resource groups, you can disable inheritance in the resource group. To disable, set Inheritance to Unique on the Security policy blade and customize the controls that Security Center shows recommendations for.

For example, if you have workloads that do not require the SQL Database Transparent Data Encryption (TDE) policy, turn off the policy at the subscription level and enable it only in the resources groups where SQL TDE is required.

> [!NOTE]
> If there is a conflict between subscription level policy and resource group level policy, the resource group level policy takes precedence.
>
>

Security Center analyzes the security state of your Azure resources. When Security Center identifies potential security vulnerabilities, it creates recommendations based on the controls set in the security policy. The recommendations guide you through the process of configuring the needed security controls.

Current policy recommendations in Security Center focus on system updates, OS configuration, network security groups on subnets and virtual machines (VMs), SQL Database Auditing, SQL Database TDE, and web application firewalls. For the most up-to-date coverage of Security Center recommendations, see [Managing security recommendations in Security Center](security-center-recommendations.md).

## <a name="scenario"></a>Scenario
This scenario shows you how to use Security Center to help reduce the chances of a significant security incident by monitoring Security Center recommendations and taking action. The scenario uses the fictitious company, Contoso, and roles presented in the Security Center [planning and operations guide](security-center-planning-and-operations-guide.md#security-roles-and-access-controls). The roles represent individuals and teams that may use Security Center to perform different security-related tasks. The roles are:

![Scenario roles][2]

Contoso recently migrated some of their on-premise resources to Azure. Contoso wants to implement and maintain protections that reduce their vulnerability to a security attack of their resources in the cloud.

## <a name="recommended-solution"></a>Recommended solution
A solution is to use Security Center to prevent and detect security vulnerabilities. Contoso has access to Security Center via their Azure subscription. The [Free tier](security-center-pricing.md) of Security Center is automatically enabled on all Azure subscriptions and data collection is enabled on all VMs in their subscription.

David, in Contoso’s IT Security, configures a **security policy** using Security Center. Security Center analyzes the security state of Contoso’s Azure resources. When Security Center identifies potential security vulnerabilities, it creates **recommendations** based on the controls set in the security policy.

Jeff, a cloud workload owner, is responsible for implementing and maintaining protections in accordance with Contoso’s security policies. Jeff can monitor the recommendations created by Security Center to apply protections. The recommendations guide Jeff through the process of configuring the needed security controls.

In order for Jeff to implement and maintain protections and eliminate security vulnerabilities, he needs to:

- Monitor security recommendations provided by Security Center
- Evaluate security recommendations and decide if he should apply or dismiss
- Apply security recommendations

Let’s follow Jeff’s steps to see how he uses Security Center recommendations to guide him through the process of configuring controls to eliminate security vulnerabilities.

## <a name="how-to-implement-this-solution"></a>How to implement this solution
Jeff signs in to [Azure portal](https://azure.microsoft.com/features/azure-portal/) and opens the Security Center console. As part of his daily monitoring activities, he checks to see if there are security recommendations by performing the following steps:

1. Jeff selects the **Recommendations** tile to open the **Recommendations** blade.
   ![Select the recommendations tile][3]
2. Jeff reviews the list of recommendations. He sees that Security Center has provided the list of recommendations in priority order, from highest priority to lowest priority. He decides to address the first High priority recommendation on the list. He selects **Install Endpoint Protection** on the **Recommendations** blade.
3. The **Install Endpoint Protection** blade opens displaying a list of VMs without antimalware enabled. Jeff reviews the list of VMs, selects all VMs, and then selects **Install on 3 VMs**.
   ![Install endpoint protection][4]
4. The **Select Endpoint Protection** blade opens providing Jeff with two antimalware solutions. Jeff selects the **Microsoft Antimalware** solution.
5. Additional information about the antimalware solution is displayed. Jeff selects **Create**.
   ![Microsoft antimalware][5]
6. Jeff enters the required configuration settings on the **Install** blade and selects **OK**.

[Microsoft Antimalware](../security/azure-security-antimalware.md) is now active on the selected VMs.

Jeff continues to move through the high priority and medium priority recommendations, making decisions on implementation. Jeff references the [Managing security recommendations](security-center-recommendations.md) article to understand the recommendations and what each one does if he applies it.

Jeff learns that [Microsoft Security Response Center (MSRC)](../security/azure-security-response-center.md) performs select security monitoring of the Azure network and infrastructure and receives threat intelligence and abuse complaints from third parties. If Jeff provides security contact details for Contoso’s Azure subscription, Microsoft contacts Contoso if the MSRC discovers that Contoso’s customer data has been accessed by an unlawful or unauthorized party. Let’s follow Jeff as he applies the **Provide security contact details** recommendation (a recommendation with severity of Medium in the list of recommendations above).

1. Jeff selects **Provide security contact details** on the **Recommendations** blade, which opens the **Provide security contact details** blade.
2. Jeff selects the Azure subscription to provide contact information on. A second **Provide security contact details** blade opens.
   ![Security contact details][6]
3. On the second **Provide security contact details** blade, Jeff enters:

  - the security contact email addresses separated by commas (there is not a limit to the number of email addresses that he can enter)
  - one security contact phone number

4. Jeff also turns on the option **Send me emails about alerts** to receive emails about high severity alerts.
5. Jeff selects **OK** to apply the security contact information to Contoso’s subscription.

Finally, Jeff reviews the low priority recommendation **Remediate OS vulnerabilities** and determines that this recommendation is not applicable. He wants to dismiss the recommendation. Jeff selects the three dots that appear to the right, and then selects **Dismiss**.
   ![Dismiss recommendation][7]

## <a name="conclusion"></a>Conclusion
Monitoring recommendations in Security Center may help you eliminate security vulnerabilities before an attack occurs. You can prevent a security incident by implementing and maintaining protections with security policies in Security Center.

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-using-recommendations/security-center-policy-inheritance.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-using-recommendations/scenario-roles.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-using-recommendations/select-recommendations-tile.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-using-recommendations/install-endpoint-protection.png
[5]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-using-recommendations/microsoft-antimalware.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-using-recommendations/provide-security-contact-details.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-using-recommendations/dismiss-recommendation.png







