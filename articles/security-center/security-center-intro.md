---
title: Introduction to Azure Security Center | Microsoft Docs
description: Learn about Azure Security Center, its key capabilities, and how it works.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: ''
ms.assetid: 45b9756b-6449-49ec-950b-5ed1e7c56daa
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/05/2017
ms.author: terrylan
ms.openlocfilehash: e0e13f5cdc3c794f3080d345f7f79f28c3ccb779
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556725"
---
# <a name="introduction-to-azure-security-center"></a>Introduction to Azure Security Center
Learn about Azure Security Center, its key capabilities, and how it works.

> [!NOTE]
> This document introduces the service by using an example deployment.
>
>

## <a name="what-is-azure-security-center"></a>What is Azure Security Center?
 Security Center helps you prevent, detect, and respond to threats with increased visibility into and control over the security of your Azure resources. It provides integrated security monitoring and policy management across your Azure subscriptions, helps detect threats that might otherwise go unnoticed, and works with a broad ecosystem of security solutions.

## <a name="key-capabilities"></a>Key capabilities
 Security Center delivers easy-to-use and effective threat prevention, detection, and response capabilities that are built in to Azure. Key capabilities are:

| Stage | Capability |
| --- | --- |
| Prevent |Monitors the security state of your Azure resources |
| Prevent | Defines policies for your Azure subscriptions and resource groups based on your company’s security requirements, the types of applications that you use, and the sensitivity of your data |
| Prevent | Uses policy-driven security recommendations to guide service owners through the process of implementing needed controls |
| Prevent | Rapidly deploys security services and appliances from Microsoft and partners |
| Detect |Automatically collects and analyzes security data from your Azure resources, the network, and partner solutions like antimalware programs and firewalls |
| Detect | Leverages global threat intelligence from Microsoft products and services, the Microsoft Digital Crimes Unit (DCU), the Microsoft Security Response Center (MSRC), and external feeds |
| Detect | Applies advanced analytics, including machine learning and behavioral analysis |
| Respond |Provides prioritized security incidents/alerts |
| Respond | Offers insights into the source of the attack and impacted resources |
| Respond | Suggests ways to stop the current attack and help prevent future attacks |

## <a name="introductory-walkthrough"></a>Introductory walkthrough
 You access Security Center from the [Azure portal](https://azure.microsoft.com/features/azure-portal/). [Sign in to the portal](https://portal.azure.com). Under the main portal menu, scroll to the **Security Center** option or select the **Security Center** tile that you previously pinned to the portal dashboard.

![Security tile in Azure portal][1]

From Security Center, you can set security policies, monitor security configurations, and view security alerts.

### <a name="security-policies"></a>Security policies
You can define policies for your Azure subscriptions and resource groups according to your company's security requirements. You can also tailor them to the types of applications you're using or to the sensitivity of the data in each subscription. For example, resources used for development or testing may have different security requirements than those used for production applications. Likewise, applications with regulated data like PII may require a higher level of security.

> [!NOTE]
> To modify a security policy at the subscription level or the resource group level, you must be the Owner of the subscription or a Contributor to it.
>
>

On the **Security Center** blade, select the **Policy** tile for a list of your subscriptions and resource groups.   

![Security Center blade][2]

On the **Security policy** blade, select a subscription to view the policy details.

![Security policy blade subscription][3]

**Data collection** (see above) enables data collection for a security policy. Enabling provides:

* Daily scanning of all supported virtual machines (VMs) for security monitoring and recommendations.
* Collection of security events for analysis and threat detection.

**Choose a storage account per region** (see above) lets you choose, for each region in which you have VMs running, the storage account where data collected from those VMs is stored. If you do not choose a storage account for each region, it is created for you. The data that's collected is logically isolated from other customers’ data for security reasons.

> [!NOTE]
> Data collection and choosing a storage account per region is configured at the subscription level.
>
>

Select **Prevention policy** (see above) to open the **Prevention policy** blade. **Show recommendations for** lets you choose the security controls that you want to monitor and the recommendations that you want to see based on the security needs of the resources within the subscription.

Next, select a resource group to view policy details.

![Security policy blade resource group][4]

**Inheritance** (see above) lets you define the resource group as:

* Inherited (default) which means all security policies for this resource group are inherited from the subscription level.
* Unique which means the resource group has a custom security policy. You need to make changes under **Show recommendations for**.

> [!NOTE]
> If there is a conflict between subscription level policy and resource group level policy, the resource group level policy takes precedence.
>
>

### <a name="security-recommendations"></a>Security recommendations
 Security Center analyzes the security state of your Azure resources to identify potential security vulnerabilities. A list of recommendations guides you through the process of configuring needed controls. Examples include:

* Provisioning antimalware to help identify and remove malicious software
* Configuring network security groups and rules to control traffic to VMs
* Provisioning of web application firewalls to help defend against attacks that target your web applications
* Deploying missing system updates
* Addressing OS configurations that do not match the recommended baselines

Click the **Recommendations** tile for a list of recommendations. Click each recommendation to view additional information or to take action to resolve the issue.

![Security recommendations in Azure Security Center][5]

### <a name="resource-health"></a>Resource health
The **Resource security health** tile shows the overall security posture of the environment by resource type, including VMs, web applications, and other resources.   

Select a resource type on the **Resource security health** tile to view more information, including a list of any potential security vulnerabilities that have been identified. (**Compute** is selected in the example below.)

![Resources health tile][6]

### <a name="security-alerts"></a>Security alerts
 Security Center automatically collects, analyzes, and integrates log data from your Azure resources, the network, and partner solutions like antimalware programs and firewalls. When threats are detected, a security alert is created. Examples include detection of:

* Compromised VMs communicating with known malicious IP addresses
* Advanced malware detected by using Windows error reporting
* Brute force attacks against VMs
* Security alerts from integrated antimalware programs and firewalls

Clicking the **Security alerts** tile displays a list of prioritized alerts.

![Security alerts][7]

Selecting an alert shows more information about the attack and suggestions for how to remediate it.

![Security alert details][8]

### <a name="partner-solutions"></a>Partner solutions
The **Partner solutions** tile lets you monitor at a glance the health status of your partner solutions integrated with your Azure subscription. Security Center displays alerts coming from the solutions.

Select the **Partner solutions** tile. A blade opens displaying a list of all connected partner solutions.

![Partner solutions][9]

## <a name="get-started"></a>Get started
To get started with Security Center, you need a subscription to Microsoft Azure. Security Center is enabled with your Azure subscription. If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).

 You access Security Center from the [Azure portal](https://azure.microsoft.com/features/azure-portal/). See the [portal documentation](https://azure.microsoft.com/documentation/services/azure-portal/) to learn more.

[Getting started with Azure Security Center](security-center-get-started.md) quickly guides you through the security-monitoring and policy-management components of Security Center.

## <a name="see-also"></a>See also
In this document, you were introduced to Security Center, its key capabilities, and how to get started. To learn more, see the following:

* [Setting security policies in Azure Security Center](security-center-policies.md) — Learn how to configure security policies for your Azure subscriptions and resource groups.
* [Managing security recommendations in Azure Security Center](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.
* [Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how to monitor the health of your Azure resources.
* [Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts.
* [Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) — Learn how to monitor the health status of your partner solutions.
* [Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.
* [Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Get the latest Azure security news and information.

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-intro/security-tile.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-intro/security-center.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-intro/security-policy.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-intro/security-policy-blade.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-intro/recommendations.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-intro/resources-health.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-intro/security-alert.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-intro/security-alert-detail.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-intro/partner-solutions.png









