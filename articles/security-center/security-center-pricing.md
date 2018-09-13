---
title: Security Center pricing | Microsoft Docs
description: This article provides information on pricing for Azure Security Center.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: ''
ms.assetid: 4d1364cd-7847-425a-bb3a-722cb0779f78
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/22/2017
ms.author: terrylan
ms.openlocfilehash: b49b08b10e62f4dc57cfb6432da8e6b04571d408
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550116"
---
# <a name="azure-security-center-pricing"></a>Azure Security Center pricing
Azure Security Center helps you prevent, detect, and respond to threats with increased visibility into and control over the security of your Azure resources. It provides integrated security monitoring and policy management across your Azure subscriptions, helps detect threats that might otherwise go unnoticed, and works with a broad ecosystem of security solutions.

## <a name="pricing-tiers"></a>Pricing tiers
Security Center is offered in two tiers:

* The **Free tier** is automatically enabled on all Azure subscriptions. The Free tier provides visibility into the security state of your Azure resources, basic security policy, security recommendations, and integration with security products and services from partners.
* The **Standard tier** adds advanced threat detection capabilities, including threat intelligence, behavioral analysis, anomaly detection, security incidents, and threat assessment reports. The Standard tier is offered free for the first 60 days.

For more information, see the Security Center [pricing page](https://azure.microsoft.com/pricing/details/security-center/).

> [!NOTE]
> Security Center uses Azure storage to save security data generated from your protected nodes. Costs associated with this storage are not included in the price of the service and are charged separately at regular [Azure storage rates](https://azure.microsoft.com/pricing/details/storage/blobs/). Storage charges apply even during the 60 day free trial.
>
>

## <a name="try-standard-free-for-60-days"></a>Try Standard free for 60 days
The Standard tier is offered free for the first 60 days. At the end of 60 days, should you choose to continue using the service, we will automatically start charging for usage.

To get the Standard tier:

1. Select the **Policy** tile on the **Security Center** blade.
2. Select the subscription that you want to upgrade to Standard.
3. On the **Security policy** blade, select **Pricing tier**.
4. On the **Choose your pricing tier** blade, select **Standard**.
5. Click **Select**.

![Standard tier][1]

## <a name="why-upgrade-to-standard"></a>Why upgrade to Standard?
The Standard tier of Security Center provides all features of the Free tier plus advanced threat detection. Advanced threat detection helps identify active threats targeting your Azure resources and provides you with the insights needed to respond quickly.

Security Center employs advanced security analytics, which go far beyond signature-based approaches. Breakthroughs in big data and machine learning technologies are used to evaluate events across the entire cloud fabric – detecting threats that would be impossible to identify using manual approaches and predicting the evolution of attacks.

Security analytics that come with the Standard tier are:

* **Threat intelligence** - Looks for known bad actors by using global threat intelligence from Microsoft products and services, the Microsoft Digital Crimes Unit, the Microsoft Security Response Center, and external feeds
* **Behavioral analysis** - Applies known patterns to discover malicious behavior
* **Anomaly detection** - Uses statistical profiling to build a historical baseline. It alerts on deviations from established baselines that conform to a potential attack vector

In the **Security alerts** blade below, Security Center has detected a security **incident**. A security incident is an aggregation of all alerts for a resource that align with kill chain patterns. Selecting the security incident reveals more details about the incident and lists the related alerts. Selecting an alert provides more information about that occurrence.

![Security incident][2]

The **Network communication** alert below provides details about the alert. Details include its full description, its severity, its current state (which in this case is dismissed, meaning the user took action to dismiss it), the attacked resource, and remediation steps. There is also a list of links to Microsoft Threat Intelligence reports. These reports can be used for security remediation and defensive purposes.

![Security alert details][3]

## <a name="enable-data-collection"></a>Enable data collection
To enable virtual machine behavioral analytics, data collection must be turned on.

To validate that data collection is enabled:

1. Select the **Policy** tile. The **Security policy** blade opens listing your Azure subscriptions.
2. Select a subscription.
3. If **Data collection** is off, change it to on and save the change.

See [Enable data collection in Azure Security Center](security-center-enable-data-collection.md) for more information.

## <a name="next-steps"></a>Next steps
* In this document, you were introduced to pricing for Security Center. For additional pricing information, see the Security Center [pricing page](https://azure.microsoft.com/pricing/details/security-center/).
* To learn more about Security Center’s advanced detection capabilities, see [Azure Security Center detection capabilities](security-center-detection-capabilities.md).
* If you have questions about using Security Center, see the [Azure Security Center FAQ](security-center-faq.md).
* If you still have questions about using Security Center, or Azure, visit the [Azure Forums](https://social.msdn.microsoft.com/Forums/home?forum=AzureSecurityCenter&filter=alltypes&sort=lastpostdesc).

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-pricing/standard.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-pricing/incident.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-pricing/network-alert.png



