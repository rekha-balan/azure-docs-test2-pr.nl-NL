---
title: Azure Security Center threat intelligence report | Microsoft Docs
description: This document helps you to use Azure Security Center Threat Intelligent Reports during an investigation to find more information regarding a security alert.
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: ''
ms.assetid: 5662e312-e8c2-4736-974e-576eeb333484
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 14ea76974a0d02b433acf025954a806e5318d887
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550509"
---
# <a name="azure-security-center-threat-intelligence-report"></a><span data-ttu-id="81e0a-103">Azure Security Center Threat Intelligence Report</span><span class="sxs-lookup"><span data-stu-id="81e0a-103">Azure Security Center Threat Intelligence Report</span></span>
<span data-ttu-id="81e0a-104">This document explains how Azure Security Center Threat Intelligent Reports can help you learn more about a threat that generated a security alert.</span><span class="sxs-lookup"><span data-stu-id="81e0a-104">This document explains how Azure Security Center Threat Intelligent Reports can help you learn more about a threat that generated a security alert.</span></span>

## <a name="what-is-a-threat-intelligence-report"></a><span data-ttu-id="81e0a-105">What is a threat intelligence report?</span><span class="sxs-lookup"><span data-stu-id="81e0a-105">What is a threat intelligence report?</span></span>
<span data-ttu-id="81e0a-106">Security Center threat detection works by monitoring security information from your Azure resources, the network, and connected partner solutions.</span><span class="sxs-lookup"><span data-stu-id="81e0a-106">Security Center threat detection works by monitoring security information from your Azure resources, the network, and connected partner solutions.</span></span> <span data-ttu-id="81e0a-107">It analyzes this information, often correlating information from multiple sources, to identify threats.</span><span class="sxs-lookup"><span data-stu-id="81e0a-107">It analyzes this information, often correlating information from multiple sources, to identify threats.</span></span> <span data-ttu-id="81e0a-108">This process is part of the Security Center [detection capabilities](security-center-detection-capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="81e0a-108">This process is part of the Security Center [detection capabilities](security-center-detection-capabilities.md).</span></span>

<span data-ttu-id="81e0a-109">When Security Center identifies a threat, it will trigger a [security alert](security-center-managing-and-responding-alerts.md), which contains detailed information regarding a particular event, including suggestions for remediation.</span><span class="sxs-lookup"><span data-stu-id="81e0a-109">When Security Center identifies a threat, it will trigger a [security alert](security-center-managing-and-responding-alerts.md), which contains detailed information regarding a particular event, including suggestions for remediation.</span></span> <span data-ttu-id="81e0a-110">To assist incident response teams investigate and remediate threats, Security Center includes a threat intelligence report that contains information about the threat that was detected, including information such as the:</span><span class="sxs-lookup"><span data-stu-id="81e0a-110">To assist incident response teams investigate and remediate threats, Security Center includes a threat intelligence report that contains information about the threat that was detected, including information such as the:</span></span>

* <span data-ttu-id="81e0a-111">Attacker’s identity or associations (if this information is available)</span><span class="sxs-lookup"><span data-stu-id="81e0a-111">Attacker’s identity or associations (if this information is available)</span></span>
* <span data-ttu-id="81e0a-112">Attackers’ objectives</span><span class="sxs-lookup"><span data-stu-id="81e0a-112">Attackers’ objectives</span></span>
* <span data-ttu-id="81e0a-113">Current and historical attack campaigns (if this information is available)</span><span class="sxs-lookup"><span data-stu-id="81e0a-113">Current and historical attack campaigns (if this information is available)</span></span>
* <span data-ttu-id="81e0a-114">Attackers’ tactics, tools and procedures</span><span class="sxs-lookup"><span data-stu-id="81e0a-114">Attackers’ tactics, tools and procedures</span></span>
* <span data-ttu-id="81e0a-115">Associated indicators of compromise (IoC) such as URLs and file hashes</span><span class="sxs-lookup"><span data-stu-id="81e0a-115">Associated indicators of compromise (IoC) such as URLs and file hashes</span></span>
* <span data-ttu-id="81e0a-116">Victimology, which is the industry and geographic prevalence to assist you in determining if your Azure resources are at risk</span><span class="sxs-lookup"><span data-stu-id="81e0a-116">Victimology, which is the industry and geographic prevalence to assist you in determining if your Azure resources are at risk</span></span>
* <span data-ttu-id="81e0a-117">Mitigation and remediation information</span><span class="sxs-lookup"><span data-stu-id="81e0a-117">Mitigation and remediation information</span></span>

> [!NOTE]
> <span data-ttu-id="81e0a-118">The amount of information in any particular report will vary; the level of detail is based on the malware’s activity and prevalence.</span><span class="sxs-lookup"><span data-stu-id="81e0a-118">The amount of information in any particular report will vary; the level of detail is based on the malware’s activity and prevalence.</span></span>
>
>

<span data-ttu-id="81e0a-119">Security Center has three types of threat reports, which can vary according to the attack.</span><span class="sxs-lookup"><span data-stu-id="81e0a-119">Security Center has three types of threat reports, which can vary according to the attack.</span></span> <span data-ttu-id="81e0a-120">The reports available are:</span><span class="sxs-lookup"><span data-stu-id="81e0a-120">The reports available are:</span></span>

* <span data-ttu-id="81e0a-121">**Activity Group Report**: provides deep dives into attackers, their objectives and tactics.</span><span class="sxs-lookup"><span data-stu-id="81e0a-121">**Activity Group Report**: provides deep dives into attackers, their objectives and tactics.</span></span>
* <span data-ttu-id="81e0a-122">**Campaign Report**: focuses on details of specific attack campaigns.</span><span class="sxs-lookup"><span data-stu-id="81e0a-122">**Campaign Report**: focuses on details of specific attack campaigns.</span></span>
* <span data-ttu-id="81e0a-123">**Threat Summary Report**: covers all of the items in the previous two reports.</span><span class="sxs-lookup"><span data-stu-id="81e0a-123">**Threat Summary Report**: covers all of the items in the previous two reports.</span></span>

<span data-ttu-id="81e0a-124">This type of information is very useful during the [incident response](security-center-incident-response.md) process, where there is an ongoing investigation to understand the source of the attack, the attacker’s motivations, and what to do to mitigate this issue moving forward.</span><span class="sxs-lookup"><span data-stu-id="81e0a-124">This type of information is very useful during the [incident response](security-center-incident-response.md) process, where there is an ongoing investigation to understand the source of the attack, the attacker’s motivations, and what to do to mitigate this issue moving forward.</span></span>

## <a name="how-to-access-the-threat-intelligence-report"></a><span data-ttu-id="81e0a-125">How to access the threat intelligence report?</span><span class="sxs-lookup"><span data-stu-id="81e0a-125">How to access the threat intelligence report?</span></span>
<span data-ttu-id="81e0a-126">You can review your current alerts by looking at the **Security alerts** tile.</span><span class="sxs-lookup"><span data-stu-id="81e0a-126">You can review your current alerts by looking at the **Security alerts** tile.</span></span> <span data-ttu-id="81e0a-127">Open the Azure Portal and follow the steps below to see more details about each alert:</span><span class="sxs-lookup"><span data-stu-id="81e0a-127">Open the Azure Portal and follow the steps below to see more details about each alert:</span></span>

1. <span data-ttu-id="81e0a-128">On the Security Center dashboard, you will see the **Security alerts** tile.</span><span class="sxs-lookup"><span data-stu-id="81e0a-128">On the Security Center dashboard, you will see the **Security alerts** tile.</span></span>
2. <span data-ttu-id="81e0a-129">Click the tile to open the **Security alerts** blade that contains more details about the alerts and click in the security alert that you want to obtain more information about.</span><span class="sxs-lookup"><span data-stu-id="81e0a-129">Click the tile to open the **Security alerts** blade that contains more details about the alerts and click in the security alert that you want to obtain more information about.</span></span>

    ![Security alerts](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-threat-report/security-center-threat-report-fig1.png)
3. <span data-ttu-id="81e0a-131">In this case the **Suspicious process executed** blade shows the details about the alert as shown in the figure below:</span><span class="sxs-lookup"><span data-stu-id="81e0a-131">In this case the **Suspicious process executed** blade shows the details about the alert as shown in the figure below:</span></span>

    ![Security alert detais](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-threat-report/security-center-threat-report-fig2.png)
4. <span data-ttu-id="81e0a-133">The amount of information available for each security alert will vary according to the type of alert.</span><span class="sxs-lookup"><span data-stu-id="81e0a-133">The amount of information available for each security alert will vary according to the type of alert.</span></span> <span data-ttu-id="81e0a-134">In the **REPORTS** field you have a link to the threat intelligence report.</span><span class="sxs-lookup"><span data-stu-id="81e0a-134">In the **REPORTS** field you have a link to the threat intelligence report.</span></span> <span data-ttu-id="81e0a-135">Click on it and another browser window will appear with PDF file.</span><span class="sxs-lookup"><span data-stu-id="81e0a-135">Click on it and another browser window will appear with PDF file.</span></span>

   ![Storage selection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-threat-report/security-center-threat-report-fig3.png)

<span data-ttu-id="81e0a-137">From here you can download the PDF for this report and read more about the security issue that was detected and take actions based on the information provided.</span><span class="sxs-lookup"><span data-stu-id="81e0a-137">From here you can download the PDF for this report and read more about the security issue that was detected and take actions based on the information provided.</span></span>

## <a name="see-also"></a><span data-ttu-id="81e0a-138">See also</span><span class="sxs-lookup"><span data-stu-id="81e0a-138">See also</span></span>
<span data-ttu-id="81e0a-139">In this document, you learned how Azure Security Center Threat Intelligent Reports can help during an investigation about security alerts.</span><span class="sxs-lookup"><span data-stu-id="81e0a-139">In this document, you learned how Azure Security Center Threat Intelligent Reports can help during an investigation about security alerts.</span></span> <span data-ttu-id="81e0a-140">To learn more about Azure Security Center, see the following:</span><span class="sxs-lookup"><span data-stu-id="81e0a-140">To learn more about Azure Security Center, see the following:</span></span>

* <span data-ttu-id="81e0a-141">[Azure Security Center FAQ](security-center-faq.md).</span><span class="sxs-lookup"><span data-stu-id="81e0a-141">[Azure Security Center FAQ](security-center-faq.md).</span></span> <span data-ttu-id="81e0a-142">Find frequently asked questions about using the service.</span><span class="sxs-lookup"><span data-stu-id="81e0a-142">Find frequently asked questions about using the service.</span></span>
* [<span data-ttu-id="81e0a-143">Leveraging Azure Security Center for Incident Response</span><span class="sxs-lookup"><span data-stu-id="81e0a-143">Leveraging Azure Security Center for Incident Response</span></span>](security-center-incident-response.md)
* [<span data-ttu-id="81e0a-144">Azure Security Center detection capabilities</span><span class="sxs-lookup"><span data-stu-id="81e0a-144">Azure Security Center detection capabilities</span></span>](security-center-detection-capabilities.md)
* <span data-ttu-id="81e0a-145">[Azure Security Center planning and operations guide](security-center-planning-and-operations-guide.md).</span><span class="sxs-lookup"><span data-stu-id="81e0a-145">[Azure Security Center planning and operations guide](security-center-planning-and-operations-guide.md).</span></span> <span data-ttu-id="81e0a-146">Learn how to plan and understand the design considerations to adopt Azure Security Center.</span><span class="sxs-lookup"><span data-stu-id="81e0a-146">Learn how to plan and understand the design considerations to adopt Azure Security Center.</span></span>
* <span data-ttu-id="81e0a-147">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="81e0a-147">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md).</span></span> <span data-ttu-id="81e0a-148">Learn how to manage and respond to security alerts.</span><span class="sxs-lookup"><span data-stu-id="81e0a-148">Learn how to manage and respond to security alerts.</span></span>
* [<span data-ttu-id="81e0a-149">Handling Security Incident in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="81e0a-149">Handling Security Incident in Azure Security Center</span></span>](security-center-incident.md)
* <span data-ttu-id="81e0a-150">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/).</span><span class="sxs-lookup"><span data-stu-id="81e0a-150">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/).</span></span> <span data-ttu-id="81e0a-151">Find blog posts about Azure security and compliance.</span><span class="sxs-lookup"><span data-stu-id="81e0a-151">Find blog posts about Azure security and compliance.</span></span>



