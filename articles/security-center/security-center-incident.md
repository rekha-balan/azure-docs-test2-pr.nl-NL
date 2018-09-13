---
title: Handling security alerts in Azure Security Center | Microsoft Docs
description: This document helps you to use Azure Security Center capabilities to handle security incidents.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: ''
ms.assetid: e8feb669-8f30-49eb-ba38-046edf3f9656
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/06/2017
ms.author: yurid
ms.openlocfilehash: 374a522b254378538d3b88eeee1ef536d38097a5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554072"
---
# <a name="handling-security-incidents-in-azure-security-center"></a><span data-ttu-id="edc96-103">Handling Security Incidents in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="edc96-103">Handling Security Incidents in Azure Security Center</span></span>
<span data-ttu-id="edc96-104">Triaging and investigating security alerts can be time consuming for even the most skilled security analysts, and for many it is hard to even know where to begin.</span><span class="sxs-lookup"><span data-stu-id="edc96-104">Triaging and investigating security alerts can be time consuming for even the most skilled security analysts, and for many it is hard to even know where to begin.</span></span> <span data-ttu-id="edc96-105">By using [analytics](security-center-detection-capabilities.md) to connect the information between distinct [security alerts](security-center-managing-and-responding-alerts.md), Security Center can provide you with a single view of an attack campaign and all of the related alerts – you can quickly understand what actions the attacker took and what resources were impacted.</span><span class="sxs-lookup"><span data-stu-id="edc96-105">By using [analytics](security-center-detection-capabilities.md) to connect the information between distinct [security alerts](security-center-managing-and-responding-alerts.md), Security Center can provide you with a single view of an attack campaign and all of the related alerts – you can quickly understand what actions the attacker took and what resources were impacted.</span></span>

<span data-ttu-id="edc96-106">This document discusses how to use security alert capability in Security Center to assist you handling security incidents.</span><span class="sxs-lookup"><span data-stu-id="edc96-106">This document discusses how to use security alert capability in Security Center to assist you handling security incidents.</span></span>

## <a name="what-is-a-security-incident"></a><span data-ttu-id="edc96-107">What is a security incident?</span><span class="sxs-lookup"><span data-stu-id="edc96-107">What is a security incident?</span></span>
<span data-ttu-id="edc96-108">In Security Center, a security incident is an aggregation of all alerts for a resource that align with [kill chain](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) patterns.</span><span class="sxs-lookup"><span data-stu-id="edc96-108">In Security Center, a security incident is an aggregation of all alerts for a resource that align with [kill chain](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) patterns.</span></span> <span data-ttu-id="edc96-109">Incidents appear in the [Security Alerts](security-center-managing-and-responding-alerts.md) tile and blade.</span><span class="sxs-lookup"><span data-stu-id="edc96-109">Incidents appear in the [Security Alerts](security-center-managing-and-responding-alerts.md) tile and blade.</span></span> <span data-ttu-id="edc96-110">An Incident will reveal the list of related alerts, which enables you to obtain more information about each occurrence.</span><span class="sxs-lookup"><span data-stu-id="edc96-110">An Incident will reveal the list of related alerts, which enables you to obtain more information about each occurrence.</span></span>

## <a name="managing-security-incidents"></a><span data-ttu-id="edc96-111">Managing security incidents</span><span class="sxs-lookup"><span data-stu-id="edc96-111">Managing security incidents</span></span>
<span data-ttu-id="edc96-112">You can review your current security incidents by looking at the security alerts tile.</span><span class="sxs-lookup"><span data-stu-id="edc96-112">You can review your current security incidents by looking at the security alerts tile.</span></span> <span data-ttu-id="edc96-113">Access the Azure Portal and follow the steps below to see more details about each security incident:</span><span class="sxs-lookup"><span data-stu-id="edc96-113">Access the Azure Portal and follow the steps below to see more details about each security incident:</span></span>

1. <span data-ttu-id="edc96-114">On the Security Center dashboard, you will see the **Security alerts** tile.</span><span class="sxs-lookup"><span data-stu-id="edc96-114">On the Security Center dashboard, you will see the **Security alerts** tile.</span></span>

    ![Security alerts tile in Security Center](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-incident/security-center-incident-fig1.png)

2. <span data-ttu-id="edc96-116">Click on this tile to expand it and if a security incident is detected, it will appear under the security alerts graph as shown  below:</span><span class="sxs-lookup"><span data-stu-id="edc96-116">Click on this tile to expand it and if a security incident is detected, it will appear under the security alerts graph as shown  below:</span></span>

    ![Security incident](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-incident/security-center-incident-fig2.png)

3. <span data-ttu-id="edc96-118">Notice that the security incident description has a different icon compared to other alerts.</span><span class="sxs-lookup"><span data-stu-id="edc96-118">Notice that the security incident description has a different icon compared to other alerts.</span></span> <span data-ttu-id="edc96-119">Click on it to view more details about this incident.</span><span class="sxs-lookup"><span data-stu-id="edc96-119">Click on it to view more details about this incident.</span></span>

    ![Security incident](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-incident/security-center-incident-fig3.png)

4. <span data-ttu-id="edc96-121">On the **incident** blade you will see more details about this security incident, which includes its full description, its severity (which in this case is high), its current state (in this case it is still *active*, which implies the user hasn't taken an action to it - this can be done by right clicking on the incident in the **Security alerts** blade), the attacked resource (in this case *VM1*), the remediation steps for the incident, and in the bottom pane you have the alerts that were included in this incident.</span><span class="sxs-lookup"><span data-stu-id="edc96-121">On the **incident** blade you will see more details about this security incident, which includes its full description, its severity (which in this case is high), its current state (in this case it is still *active*, which implies the user hasn't taken an action to it - this can be done by right clicking on the incident in the **Security alerts** blade), the attacked resource (in this case *VM1*), the remediation steps for the incident, and in the bottom pane you have the alerts that were included in this incident.</span></span> <span data-ttu-id="edc96-122">If you want to obtain more information on each alert, just click on it and another blade will open, as shown below:</span><span class="sxs-lookup"><span data-stu-id="edc96-122">If you want to obtain more information on each alert, just click on it and another blade will open, as shown below:</span></span>

    ![Security incident](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-incident/security-center-incident-fig4.png)

<span data-ttu-id="edc96-124">The information on this blade will vary according to the alert.</span><span class="sxs-lookup"><span data-stu-id="edc96-124">The information on this blade will vary according to the alert.</span></span> <span data-ttu-id="edc96-125">Read [Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) for more information on how to manage these alerts.</span><span class="sxs-lookup"><span data-stu-id="edc96-125">Read [Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) for more information on how to manage these alerts.</span></span> <span data-ttu-id="edc96-126">Some important considerations regarding this capability:</span><span class="sxs-lookup"><span data-stu-id="edc96-126">Some important considerations regarding this capability:</span></span>

* <span data-ttu-id="edc96-127">A new filter enables you to customize your view to Incident only, Alerts only, or both.</span><span class="sxs-lookup"><span data-stu-id="edc96-127">A new filter enables you to customize your view to Incident only, Alerts only, or both.</span></span>
* <span data-ttu-id="edc96-128">The same alert can exist as part of an Incident (if applicable), as well as to be visible as a standalone alert.</span><span class="sxs-lookup"><span data-stu-id="edc96-128">The same alert can exist as part of an Incident (if applicable), as well as to be visible as a standalone alert.</span></span>

## <a name="see-also"></a><span data-ttu-id="edc96-129">See also</span><span class="sxs-lookup"><span data-stu-id="edc96-129">See also</span></span>
<span data-ttu-id="edc96-130">In this document, you learned how to use the security incident capability in Security Center.</span><span class="sxs-lookup"><span data-stu-id="edc96-130">In this document, you learned how to use the security incident capability in Security Center.</span></span> <span data-ttu-id="edc96-131">To learn more about Security Center, see the following:</span><span class="sxs-lookup"><span data-stu-id="edc96-131">To learn more about Security Center, see the following:</span></span>

* [<span data-ttu-id="edc96-132">Managing and responding to security alerts in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="edc96-132">Managing and responding to security alerts in Azure Security Center</span></span>](security-center-managing-and-responding-alerts.md)
* [<span data-ttu-id="edc96-133">Azure Security Center Detection Capabilities</span><span class="sxs-lookup"><span data-stu-id="edc96-133">Azure Security Center Detection Capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="edc96-134">Azure Security Center Planning and Operations Guide</span><span class="sxs-lookup"><span data-stu-id="edc96-134">Azure Security Center Planning and Operations Guide</span></span>](security-center-planning-and-operations-guide.md)
* [<span data-ttu-id="edc96-135">Managing and responding to security alerts in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="edc96-135">Managing and responding to security alerts in Azure Security Center</span></span>](security-center-managing-and-responding-alerts.md)
* <span data-ttu-id="edc96-136">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.</span><span class="sxs-lookup"><span data-stu-id="edc96-136">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="edc96-137">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Find blog posts about Azure security and compliance.</span><span class="sxs-lookup"><span data-stu-id="edc96-137">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Find blog posts about Azure security and compliance.</span></span>




