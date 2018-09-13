---
title: Partner Integration in Azure Security Center | Microsoft Docs
description: This document explains how Azure Security Center integrates with partners to enhance overall security of your Azure resources.
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: ''
ms.assetid: 6af354da-f27a-467a-8b7e-6cbcf70fdbcb
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: ffd64eeb0eb2966a949af81cf6b9526cd89b5e62
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550508"
---
# <a name="partner-integration-in-azure-security-center"></a><span data-ttu-id="d903c-103">Partner Integration in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="d903c-103">Partner Integration in Azure Security Center</span></span>
<span data-ttu-id="d903c-104">This document explains how Azure Security Center integrates with partners to enhance overall security and provide an integrated experience in Azure, while taking advantage of the Azure Marketplace for partner certification and billing.</span><span class="sxs-lookup"><span data-stu-id="d903c-104">This document explains how Azure Security Center integrates with partners to enhance overall security and provide an integrated experience in Azure, while taking advantage of the Azure Marketplace for partner certification and billing.</span></span>

## <a name="why-deploy-partners-solutions-from-security-center"></a><span data-ttu-id="d903c-105">Why deploy partner’s solutions from Security Center?</span><span class="sxs-lookup"><span data-stu-id="d903c-105">Why deploy partner’s solutions from Security Center?</span></span>

<span data-ttu-id="d903c-106">The four main reasons to leverage the partner integration in Security Center are:</span><span class="sxs-lookup"><span data-stu-id="d903c-106">The four main reasons to leverage the partner integration in Security Center are:</span></span>

- <span data-ttu-id="d903c-107">**Ease of deployment**: Deploying a partner solution by following the Security Center recommendation is much easier.</span><span class="sxs-lookup"><span data-stu-id="d903c-107">**Ease of deployment**: Deploying a partner solution by following the Security Center recommendation is much easier.</span></span> <span data-ttu-id="d903c-108">The deployment process can be fully automated using a default configuration and network topology, or customers can choose a semi-automated option to allow more flexibility and customization of the configuration.</span><span class="sxs-lookup"><span data-stu-id="d903c-108">The deployment process can be fully automated using a default configuration and network topology, or customers can choose a semi-automated option to allow more flexibility and customization of the configuration.</span></span>
- <span data-ttu-id="d903c-109">**Integrated Detections**: Security events from partner solutions are automatically collected, aggregated and displayed as part of Security Center alerts and incidents.</span><span class="sxs-lookup"><span data-stu-id="d903c-109">**Integrated Detections**: Security events from partner solutions are automatically collected, aggregated and displayed as part of Security Center alerts and incidents.</span></span> <span data-ttu-id="d903c-110">These events are also fused with detections from other sources to provide advanced threat detection capabilities.</span><span class="sxs-lookup"><span data-stu-id="d903c-110">These events are also fused with detections from other sources to provide advanced threat detection capabilities.</span></span>
- <span data-ttu-id="d903c-111">**Unified Health Monitoring and Management**: Integrated health events allow customers to monitor all partner solutions at a glance.</span><span class="sxs-lookup"><span data-stu-id="d903c-111">**Unified Health Monitoring and Management**: Integrated health events allow customers to monitor all partner solutions at a glance.</span></span> <span data-ttu-id="d903c-112">Basic management is available with easy access to advanced configuration using the partner solution.</span><span class="sxs-lookup"><span data-stu-id="d903c-112">Basic management is available with easy access to advanced configuration using the partner solution.</span></span>
- <span data-ttu-id="d903c-113">**Export to SIEM**: Customers can now export all Security Center and partners’ alerts in CEF format to on-premise SIEM systems using Microsoft Azure Log Integration (preview)</span><span class="sxs-lookup"><span data-stu-id="d903c-113">**Export to SIEM**: Customers can now export all Security Center and partners’ alerts in CEF format to on-premise SIEM systems using Microsoft Azure Log Integration (preview)</span></span>


## <a name="what-partners-are-integrated-with-security-center"></a><span data-ttu-id="d903c-114">What partners are integrated with Security Center?</span><span class="sxs-lookup"><span data-stu-id="d903c-114">What partners are integrated with Security Center?</span></span>
<span data-ttu-id="d903c-115">Security Center currently integrates with the following partners:</span><span class="sxs-lookup"><span data-stu-id="d903c-115">Security Center currently integrates with the following partners:</span></span>

- <span data-ttu-id="d903c-116">Endpoint Protection (Trend Micro),</span><span class="sxs-lookup"><span data-stu-id="d903c-116">Endpoint Protection (Trend Micro),</span></span> 
- <span data-ttu-id="d903c-117">Web Application Firewall (Barracuda, F5, Imperva and soon Microsoft WAF and Fortinet),</span><span class="sxs-lookup"><span data-stu-id="d903c-117">Web Application Firewall (Barracuda, F5, Imperva and soon Microsoft WAF and Fortinet),</span></span> 
- <span data-ttu-id="d903c-118">Next Generation Firewall (Check Point, Barracuda and soon Fortinet and Cisco) solutions.</span><span class="sxs-lookup"><span data-stu-id="d903c-118">Next Generation Firewall (Check Point, Barracuda and soon Fortinet and Cisco) solutions.</span></span> 
- <span data-ttu-id="d903c-119">Vulnerability Assessment (Qualys - preview) solutions.</span><span class="sxs-lookup"><span data-stu-id="d903c-119">Vulnerability Assessment (Qualys - preview) solutions.</span></span> 

<span data-ttu-id="d903c-120">Over time, Security Center will expand the number of partners within these existing categories and add new categories.</span><span class="sxs-lookup"><span data-stu-id="d903c-120">Over time, Security Center will expand the number of partners within these existing categories and add new categories.</span></span> 

## <a name="how-to-deploy-a-partner-solution"></a><span data-ttu-id="d903c-121">How to deploy a partner solution?</span><span class="sxs-lookup"><span data-stu-id="d903c-121">How to deploy a partner solution?</span></span>

<span data-ttu-id="d903c-122">Based on the configuration of your Azure environment and the security policy you defined, Security Center may recommend that a partner solution be deployed.</span><span class="sxs-lookup"><span data-stu-id="d903c-122">Based on the configuration of your Azure environment and the security policy you defined, Security Center may recommend that a partner solution be deployed.</span></span> <span data-ttu-id="d903c-123">The recommendation will guide you through the process of selecting and installing a partner solution.</span><span class="sxs-lookup"><span data-stu-id="d903c-123">The recommendation will guide you through the process of selecting and installing a partner solution.</span></span> <span data-ttu-id="d903c-124">The overall deployment experience at this point can vary according to the type of solution and partner.</span><span class="sxs-lookup"><span data-stu-id="d903c-124">The overall deployment experience at this point can vary according to the type of solution and partner.</span></span> <span data-ttu-id="d903c-125">See the links below for more information:</span><span class="sxs-lookup"><span data-stu-id="d903c-125">See the links below for more information:</span></span>

- [<span data-ttu-id="d903c-126">Add a web application firewall</span><span class="sxs-lookup"><span data-stu-id="d903c-126">Add a web application firewall</span></span>](security-center-add-web-application-firewall.md)
- [<span data-ttu-id="d903c-127">Add a Next Generation Firewall</span><span class="sxs-lookup"><span data-stu-id="d903c-127">Add a Next Generation Firewall</span></span>](security-center-add-next-generation-firewall.md)
- [<span data-ttu-id="d903c-128">Install Endpoint Protection</span><span class="sxs-lookup"><span data-stu-id="d903c-128">Install Endpoint Protection</span></span>](security-center-install-endpoint-protection.md)
- [<span data-ttu-id="d903c-129">Vulnerability assessment not installed</span><span class="sxs-lookup"><span data-stu-id="d903c-129">Vulnerability assessment not installed</span></span>](security-center-vulnerability-assessment-recommendations.md)

## <a name="how-to-manage-partner-solutions"></a><span data-ttu-id="d903c-130">How to manage partner solutions?</span><span class="sxs-lookup"><span data-stu-id="d903c-130">How to manage partner solutions?</span></span>

<span data-ttu-id="d903c-131">Once a partner solution has been deployed, you can view information about the health of the solution and perform basic management tasks from the Partner solution tile in the main Security Center dashboard.</span><span class="sxs-lookup"><span data-stu-id="d903c-131">Once a partner solution has been deployed, you can view information about the health of the solution and perform basic management tasks from the Partner solution tile in the main Security Center dashboard.</span></span> <span data-ttu-id="d903c-132">For more information about managing partner solutions in Security Center, read [Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="d903c-132">For more information about managing partner solutions in Security Center, read [Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md).</span></span>

![Partner Integration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-partner-integration/security-center-partner-integration-fig1-new.png)


## <a name="see-also"></a><span data-ttu-id="d903c-134">See also</span><span class="sxs-lookup"><span data-stu-id="d903c-134">See also</span></span>
<span data-ttu-id="d903c-135">In this document, you learned how to integrate partner's solution in Azure Security Center.</span><span class="sxs-lookup"><span data-stu-id="d903c-135">In this document, you learned how to integrate partner's solution in Azure Security Center.</span></span> <span data-ttu-id="d903c-136">To learn more about Security Center, see the following:</span><span class="sxs-lookup"><span data-stu-id="d903c-136">To learn more about Security Center, see the following:</span></span>

* [<span data-ttu-id="d903c-137">Azure Security Center Planning and Operations Guide</span><span class="sxs-lookup"><span data-stu-id="d903c-137">Azure Security Center Planning and Operations Guide</span></span>](security-center-planning-and-operations-guide.md)
* [<span data-ttu-id="d903c-138">Managing and responding to security alerts in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="d903c-138">Managing and responding to security alerts in Azure Security Center</span></span>](security-center-managing-and-responding-alerts.md)
* [<span data-ttu-id="d903c-139">Security Alerts by Type in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="d903c-139">Security Alerts by Type in Azure Security Center</span></span>](security-center-alerts-type.md)
* <span data-ttu-id="d903c-140">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how to monitor the health of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="d903c-140">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="d903c-141">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) — Learn how to monitor the health status of your partner solutions.</span><span class="sxs-lookup"><span data-stu-id="d903c-141">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) — Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="d903c-142">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span><span class="sxs-lookup"><span data-stu-id="d903c-142">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="d903c-143">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance.</span><span class="sxs-lookup"><span data-stu-id="d903c-143">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>

