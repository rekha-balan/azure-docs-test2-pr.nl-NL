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
# <a name="add-a-web-application-firewall-in-azure-security-center"></a><span data-ttu-id="400db-103">Add a web application firewall in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="400db-103">Add a web application firewall in Azure Security Center</span></span>
<span data-ttu-id="400db-104">Azure Security Center may recommend that you add a web application firewall (WAF) from a Microsoft partner to secure your web applications.</span><span class="sxs-lookup"><span data-stu-id="400db-104">Azure Security Center may recommend that you add a web application firewall (WAF) from a Microsoft partner to secure your web applications.</span></span> <span data-ttu-id="400db-105">This document walks you through an example of how to apply this recommendation.</span><span class="sxs-lookup"><span data-stu-id="400db-105">This document walks you through an example of how to apply this recommendation.</span></span>

<span data-ttu-id="400db-106">A WAF recommendation is shown for any public facing IP (either Instance Level IP or Load Balanced IP) that has an associated network security group with open inbound web ports (80,443).</span><span class="sxs-lookup"><span data-stu-id="400db-106">A WAF recommendation is shown for any public facing IP (either Instance Level IP or Load Balanced IP) that has an associated network security group with open inbound web ports (80,443).</span></span>

<span data-ttu-id="400db-107">Security Center recommends that you provision a WAF to help defend against attacks targeting your web applications on virtual machines and on App Service Environment.</span><span class="sxs-lookup"><span data-stu-id="400db-107">Security Center recommends that you provision a WAF to help defend against attacks targeting your web applications on virtual machines and on App Service Environment.</span></span> <span data-ttu-id="400db-108">An App Service Environment (ASE) is a [Premium](https://azure.microsoft.com/pricing/details/app-service/) service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps.</span><span class="sxs-lookup"><span data-stu-id="400db-108">An App Service Environment (ASE) is a [Premium](https://azure.microsoft.com/pricing/details/app-service/) service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps.</span></span> <span data-ttu-id="400db-109">To learn more about ASE, see the [App Service Environment Documentation](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="400db-109">To learn more about ASE, see the [App Service Environment Documentation](../app-service/app-service-app-service-environments-readme.md).</span></span>

> [!NOTE]
> <span data-ttu-id="400db-110">This document introduces the service by using an example deployment.</span><span class="sxs-lookup"><span data-stu-id="400db-110">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="400db-111">This document is not a step-by-step guide.</span><span class="sxs-lookup"><span data-stu-id="400db-111">This document is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="400db-112">Implement the recommendation</span><span class="sxs-lookup"><span data-stu-id="400db-112">Implement the recommendation</span></span>
1. <span data-ttu-id="400db-113">In the **Recommendations** blade, select **Secure web application using web application firewall**.</span><span class="sxs-lookup"><span data-stu-id="400db-113">In the **Recommendations** blade, select **Secure web application using web application firewall**.</span></span>
   <span data-ttu-id="400db-114">![Secure web Application][1]</span><span class="sxs-lookup"><span data-stu-id="400db-114">![Secure web Application][1]</span></span>
2. <span data-ttu-id="400db-115">In the **Secure your web applications using web application firewall** blade, select a web application.</span><span class="sxs-lookup"><span data-stu-id="400db-115">In the **Secure your web applications using web application firewall** blade, select a web application.</span></span> <span data-ttu-id="400db-116">The **Add a Web Application Firewall** blade opens.</span><span class="sxs-lookup"><span data-stu-id="400db-116">The **Add a Web Application Firewall** blade opens.</span></span>
   <span data-ttu-id="400db-117">![Add a web application firewall][2]</span><span class="sxs-lookup"><span data-stu-id="400db-117">![Add a web application firewall][2]</span></span>
3. <span data-ttu-id="400db-118">You can choose to use an existing web application firewall if available or you can create a new one.</span><span class="sxs-lookup"><span data-stu-id="400db-118">You can choose to use an existing web application firewall if available or you can create a new one.</span></span> <span data-ttu-id="400db-119">In this example, there are no existing WAFs available so we create a WAF.</span><span class="sxs-lookup"><span data-stu-id="400db-119">In this example, there are no existing WAFs available so we create a WAF.</span></span>
4. <span data-ttu-id="400db-120">To create a WAF, select a solution from the list of integrated partners.</span><span class="sxs-lookup"><span data-stu-id="400db-120">To create a WAF, select a solution from the list of integrated partners.</span></span> <span data-ttu-id="400db-121">In this example, we select **Barracuda Web Application Firewall**.</span><span class="sxs-lookup"><span data-stu-id="400db-121">In this example, we select **Barracuda Web Application Firewall**.</span></span>
5. <span data-ttu-id="400db-122">The **Barracuda Web Application Firewall** blade opens providing you information about the partner solution.</span><span class="sxs-lookup"><span data-stu-id="400db-122">The **Barracuda Web Application Firewall** blade opens providing you information about the partner solution.</span></span> <span data-ttu-id="400db-123">Select **Create** in the information blade.</span><span class="sxs-lookup"><span data-stu-id="400db-123">Select **Create** in the information blade.</span></span>
   <span data-ttu-id="400db-124">![Firewall information blade][3]</span><span class="sxs-lookup"><span data-stu-id="400db-124">![Firewall information blade][3]</span></span>
6. <span data-ttu-id="400db-125">The **New Web Application Firewall** blade opens, where you can perform **VM Configuration** steps and provide **WAF Information**.</span><span class="sxs-lookup"><span data-stu-id="400db-125">The **New Web Application Firewall** blade opens, where you can perform **VM Configuration** steps and provide **WAF Information**.</span></span> <span data-ttu-id="400db-126">Select **VM Configuration**.</span><span class="sxs-lookup"><span data-stu-id="400db-126">Select **VM Configuration**.</span></span>
7. <span data-ttu-id="400db-127">In the **VM Configuration** blade, you enter information required to spin up the virtual machine that runs the WAF.</span><span class="sxs-lookup"><span data-stu-id="400db-127">In the **VM Configuration** blade, you enter information required to spin up the virtual machine that runs the WAF.</span></span>
   <span data-ttu-id="400db-128">![VM configuration][4]</span><span class="sxs-lookup"><span data-stu-id="400db-128">![VM configuration][4]</span></span>
8. <span data-ttu-id="400db-129">Return to the **New Web Application Firewall** blade and select **WAF Information**.</span><span class="sxs-lookup"><span data-stu-id="400db-129">Return to the **New Web Application Firewall** blade and select **WAF Information**.</span></span> <span data-ttu-id="400db-130">In the **WAF Information** blade, you configure the WAF itself.</span><span class="sxs-lookup"><span data-stu-id="400db-130">In the **WAF Information** blade, you configure the WAF itself.</span></span> <span data-ttu-id="400db-131">Step 7 allows you to configure the virtual machine on which the WAF runs and step 8 enables you to provision the WAF itself.</span><span class="sxs-lookup"><span data-stu-id="400db-131">Step 7 allows you to configure the virtual machine on which the WAF runs and step 8 enables you to provision the WAF itself.</span></span>

## <a name="finalize-application-protection"></a><span data-ttu-id="400db-132">Finalize application protection</span><span class="sxs-lookup"><span data-stu-id="400db-132">Finalize application protection</span></span>
1. <span data-ttu-id="400db-133">Return to the **Recommendations** blade.</span><span class="sxs-lookup"><span data-stu-id="400db-133">Return to the **Recommendations** blade.</span></span> <span data-ttu-id="400db-134">A new entry was generated after you created the WAF, called **Finalize application protection**.</span><span class="sxs-lookup"><span data-stu-id="400db-134">A new entry was generated after you created the WAF, called **Finalize application protection**.</span></span> <span data-ttu-id="400db-135">This entry lets you know that you need to complete the process of actually wiring up the WAF within the Azure Virtual Network so that it can protect the application.</span><span class="sxs-lookup"><span data-stu-id="400db-135">This entry lets you know that you need to complete the process of actually wiring up the WAF within the Azure Virtual Network so that it can protect the application.</span></span>
   <span data-ttu-id="400db-136">![Finalize application protection][5]</span><span class="sxs-lookup"><span data-stu-id="400db-136">![Finalize application protection][5]</span></span>
2. <span data-ttu-id="400db-137">Select **Finalize application protection**.</span><span class="sxs-lookup"><span data-stu-id="400db-137">Select **Finalize application protection**.</span></span> <span data-ttu-id="400db-138">A new blade opens.</span><span class="sxs-lookup"><span data-stu-id="400db-138">A new blade opens.</span></span> <span data-ttu-id="400db-139">You can see that there is a web application that needs to have its traffic rerouted.</span><span class="sxs-lookup"><span data-stu-id="400db-139">You can see that there is a web application that needs to have its traffic rerouted.</span></span>
3. <span data-ttu-id="400db-140">Select the web application.</span><span class="sxs-lookup"><span data-stu-id="400db-140">Select the web application.</span></span> <span data-ttu-id="400db-141">A blade opens that gives you steps for finalizing the web application firewall setup.</span><span class="sxs-lookup"><span data-stu-id="400db-141">A blade opens that gives you steps for finalizing the web application firewall setup.</span></span> <span data-ttu-id="400db-142">Complete the steps, and then select **Restrict traffic**.</span><span class="sxs-lookup"><span data-stu-id="400db-142">Complete the steps, and then select **Restrict traffic**.</span></span> <span data-ttu-id="400db-143">Security Center then does the wiring-up for you.</span><span class="sxs-lookup"><span data-stu-id="400db-143">Security Center then does the wiring-up for you.</span></span>
   <span data-ttu-id="400db-144">![Restrict traffic][6]</span><span class="sxs-lookup"><span data-stu-id="400db-144">![Restrict traffic][6]</span></span>

> [!NOTE]
> <span data-ttu-id="400db-145">You can protect multiple web applications in Security Center by adding these applications to your existing WAF deployments.</span><span class="sxs-lookup"><span data-stu-id="400db-145">You can protect multiple web applications in Security Center by adding these applications to your existing WAF deployments.</span></span>
>
>

<span data-ttu-id="400db-146">The logs from that WAF are now fully integrated.</span><span class="sxs-lookup"><span data-stu-id="400db-146">The logs from that WAF are now fully integrated.</span></span> <span data-ttu-id="400db-147">Security Center can start automatically gathering and analyzing the logs so that it can surface important security alerts to you.</span><span class="sxs-lookup"><span data-stu-id="400db-147">Security Center can start automatically gathering and analyzing the logs so that it can surface important security alerts to you.</span></span>

## <a name="see-also"></a><span data-ttu-id="400db-148">See also</span><span class="sxs-lookup"><span data-stu-id="400db-148">See also</span></span>
<span data-ttu-id="400db-149">This document showed you how to implement the Security Center recommendation "Add a web application."</span><span class="sxs-lookup"><span data-stu-id="400db-149">This document showed you how to implement the Security Center recommendation "Add a web application."</span></span> <span data-ttu-id="400db-150">To learn more about configuring a web application firewall, see the following:</span><span class="sxs-lookup"><span data-stu-id="400db-150">To learn more about configuring a web application firewall, see the following:</span></span>

* [<span data-ttu-id="400db-151">Configuring a Web Application Firewall (WAF) for App Service Environment</span><span class="sxs-lookup"><span data-stu-id="400db-151">Configuring a Web Application Firewall (WAF) for App Service Environment</span></span>](../app-service-web/app-service-app-service-environment-web-application-firewall.md)

<span data-ttu-id="400db-152">To learn more about Security Center, see the following:</span><span class="sxs-lookup"><span data-stu-id="400db-152">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="400db-153">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span><span class="sxs-lookup"><span data-stu-id="400db-153">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="400db-154">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="400db-154">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="400db-155">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span><span class="sxs-lookup"><span data-stu-id="400db-155">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="400db-156">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="400db-156">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="400db-157">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span><span class="sxs-lookup"><span data-stu-id="400db-157">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="400db-158">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span><span class="sxs-lookup"><span data-stu-id="400db-158">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-add-web-application-firewall/secure-web-application.png
[2]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-add-web-application-firewall/add-a-waf.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-add-web-application-firewall/info-blade.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-add-web-application-firewall/select-vm-config.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-add-web-application-firewall/finalize-waf.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-add-web-application-firewall/restrict-traffic.png






