---
title: Add a next generation firewall in Azure Security Center | Microsoft Docs
description: This document shows you how to implement the Azure Security Center recommendations **Add a Next Generation Firewall** and **Route traffice through NGFW only**.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: ''
ms.assetid: 48b99015-4db8-4ce8-85e4-b544c0fa203e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 17a52a88bcd8abbe2fad8e03874e84648c1d4f58
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564499"
---
# <a name="add-a-next-generation-firewall-in-azure-security-center"></a><span data-ttu-id="e3453-103">Add a Next Generation Firewall in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="e3453-103">Add a Next Generation Firewall in Azure Security Center</span></span>
<span data-ttu-id="e3453-104">Azure Security Center may recommend that you add a next generation firewall (NGFW) from a Microsoft partner to increase your security protections.</span><span class="sxs-lookup"><span data-stu-id="e3453-104">Azure Security Center may recommend that you add a next generation firewall (NGFW) from a Microsoft partner to increase your security protections.</span></span> <span data-ttu-id="e3453-105">This document walks you through an example of how to do this.</span><span class="sxs-lookup"><span data-stu-id="e3453-105">This document walks you through an example of how to do this.</span></span>

> [!NOTE]
> <span data-ttu-id="e3453-106">This document introduces the service by using an example deployment.</span><span class="sxs-lookup"><span data-stu-id="e3453-106">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="e3453-107">This is not a step-by-step guide.</span><span class="sxs-lookup"><span data-stu-id="e3453-107">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="e3453-108">Implement the recommendation</span><span class="sxs-lookup"><span data-stu-id="e3453-108">Implement the recommendation</span></span>
1. <span data-ttu-id="e3453-109">In the **Recommendations** blade, select **Add a Next Generation Firewall**.</span><span class="sxs-lookup"><span data-stu-id="e3453-109">In the **Recommendations** blade, select **Add a Next Generation Firewall**.</span></span>
   <span data-ttu-id="e3453-110">![Add a Next Generation Firewall][1]</span><span class="sxs-lookup"><span data-stu-id="e3453-110">![Add a Next Generation Firewall][1]</span></span>
2. <span data-ttu-id="e3453-111">In the **Add a Next Generation Firewall** blade, select an endpoint.</span><span class="sxs-lookup"><span data-stu-id="e3453-111">In the **Add a Next Generation Firewall** blade, select an endpoint.</span></span>
   <span data-ttu-id="e3453-112">![Select an endpoint][2]</span><span class="sxs-lookup"><span data-stu-id="e3453-112">![Select an endpoint][2]</span></span>
3. <span data-ttu-id="e3453-113">A second **Add a Next Generation Firewall** blade opens.</span><span class="sxs-lookup"><span data-stu-id="e3453-113">A second **Add a Next Generation Firewall** blade opens.</span></span> <span data-ttu-id="e3453-114">You can choose to use an existing solution if available or you can create a new one.</span><span class="sxs-lookup"><span data-stu-id="e3453-114">You can choose to use an existing solution if available or you can create a new one.</span></span> <span data-ttu-id="e3453-115">In this example, there are no existing solutions available so we create an NGFW.</span><span class="sxs-lookup"><span data-stu-id="e3453-115">In this example, there are no existing solutions available so we create an NGFW.</span></span>
   <span data-ttu-id="e3453-116">![Create Next Generation Firewall][3]</span><span class="sxs-lookup"><span data-stu-id="e3453-116">![Create Next Generation Firewall][3]</span></span>
4. <span data-ttu-id="e3453-117">To create an NGFW, select a solution from the list of integrated partners.</span><span class="sxs-lookup"><span data-stu-id="e3453-117">To create an NGFW, select a solution from the list of integrated partners.</span></span> <span data-ttu-id="e3453-118">In this example, we select **Check Point**.</span><span class="sxs-lookup"><span data-stu-id="e3453-118">In this example, we select **Check Point**.</span></span>
   <span data-ttu-id="e3453-119">![Select Next Generation Firewall solution][4]</span><span class="sxs-lookup"><span data-stu-id="e3453-119">![Select Next Generation Firewall solution][4]</span></span>
5. <span data-ttu-id="e3453-120">The **Check Point** blade opens providing you information about the partner solution.</span><span class="sxs-lookup"><span data-stu-id="e3453-120">The **Check Point** blade opens providing you information about the partner solution.</span></span> <span data-ttu-id="e3453-121">Select **Create** in the information blade.</span><span class="sxs-lookup"><span data-stu-id="e3453-121">Select **Create** in the information blade.</span></span>
   <span data-ttu-id="e3453-122">![Firewall information blade][5]</span><span class="sxs-lookup"><span data-stu-id="e3453-122">![Firewall information blade][5]</span></span>
6. <span data-ttu-id="e3453-123">The **Create virtual machine** blade opens.</span><span class="sxs-lookup"><span data-stu-id="e3453-123">The **Create virtual machine** blade opens.</span></span> <span data-ttu-id="e3453-124">Here you can enter information required to spin up a virtual machine (VM) that runs the NGFW.</span><span class="sxs-lookup"><span data-stu-id="e3453-124">Here you can enter information required to spin up a virtual machine (VM) that runs the NGFW.</span></span> <span data-ttu-id="e3453-125">Follow the steps and provide the NGFW information required.</span><span class="sxs-lookup"><span data-stu-id="e3453-125">Follow the steps and provide the NGFW information required.</span></span> <span data-ttu-id="e3453-126">Select OK to apply.</span><span class="sxs-lookup"><span data-stu-id="e3453-126">Select OK to apply.</span></span>
   <span data-ttu-id="e3453-127">![Create virtual machine to run NGFW][6]</span><span class="sxs-lookup"><span data-stu-id="e3453-127">![Create virtual machine to run NGFW][6]</span></span>

## <a name="route-traffic-through-ngfw-only"></a><span data-ttu-id="e3453-128">Route traffic through NGFW only</span><span class="sxs-lookup"><span data-stu-id="e3453-128">Route traffic through NGFW only</span></span>
<span data-ttu-id="e3453-129">Return to the **Recommendations** blade.</span><span class="sxs-lookup"><span data-stu-id="e3453-129">Return to the **Recommendations** blade.</span></span> <span data-ttu-id="e3453-130">A new entry was generated after you added an NGFW via Security Center, called **Route traffic through NGFW only**.</span><span class="sxs-lookup"><span data-stu-id="e3453-130">A new entry was generated after you added an NGFW via Security Center, called **Route traffic through NGFW only**.</span></span> <span data-ttu-id="e3453-131">This recommendation is created only if you installed your NGFW through Security Center.</span><span class="sxs-lookup"><span data-stu-id="e3453-131">This recommendation is created only if you installed your NGFW through Security Center.</span></span> <span data-ttu-id="e3453-132">If you have Internet-facing endpoints, Security Center recommends that you configure Network Security Group rules that force inbound traffic to your VM through your NGFW.</span><span class="sxs-lookup"><span data-stu-id="e3453-132">If you have Internet-facing endpoints, Security Center recommends that you configure Network Security Group rules that force inbound traffic to your VM through your NGFW.</span></span>

1. <span data-ttu-id="e3453-133">In the **Recommendations blade**, select **Route traffic through NGFW only**.</span><span class="sxs-lookup"><span data-stu-id="e3453-133">In the **Recommendations blade**, select **Route traffic through NGFW only**.</span></span>
   <span data-ttu-id="e3453-134">![Route traffic through NGFW only][7]</span><span class="sxs-lookup"><span data-stu-id="e3453-134">![Route traffic through NGFW only][7]</span></span>
2. <span data-ttu-id="e3453-135">This opens the blade **Route traffic through NGFW only**, which lists VMs that you can route traffic to.</span><span class="sxs-lookup"><span data-stu-id="e3453-135">This opens the blade **Route traffic through NGFW only**, which lists VMs that you can route traffic to.</span></span> <span data-ttu-id="e3453-136">Select a VM from the list.</span><span class="sxs-lookup"><span data-stu-id="e3453-136">Select a VM from the list.</span></span>
   <span data-ttu-id="e3453-137">![Select a VM][8]</span><span class="sxs-lookup"><span data-stu-id="e3453-137">![Select a VM][8]</span></span>
3. <span data-ttu-id="e3453-138">A blade for the selected VM opens, displaying related inbound rules.</span><span class="sxs-lookup"><span data-stu-id="e3453-138">A blade for the selected VM opens, displaying related inbound rules.</span></span> <span data-ttu-id="e3453-139">A description provides you with more information on possible next steps.</span><span class="sxs-lookup"><span data-stu-id="e3453-139">A description provides you with more information on possible next steps.</span></span> <span data-ttu-id="e3453-140">Select **Edit inbound rules** to proceed with editing an inbound rule.</span><span class="sxs-lookup"><span data-stu-id="e3453-140">Select **Edit inbound rules** to proceed with editing an inbound rule.</span></span> <span data-ttu-id="e3453-141">The expectation is that **Source** is not set to **Any** for the Internet-facing endpoints linked with the NGFW.</span><span class="sxs-lookup"><span data-stu-id="e3453-141">The expectation is that **Source** is not set to **Any** for the Internet-facing endpoints linked with the NGFW.</span></span> <span data-ttu-id="e3453-142">To learn more about the properties of the inbound rule, see [NSG rules](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span><span class="sxs-lookup"><span data-stu-id="e3453-142">To learn more about the properties of the inbound rule, see [NSG rules](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span></span>
   <span data-ttu-id="e3453-143">![Configure rules to limit access][9]
   ![Edit inbound rule][10]</span><span class="sxs-lookup"><span data-stu-id="e3453-143">![Configure rules to limit access][9]
![Edit inbound rule][10]</span></span>

## <a name="see-also"></a><span data-ttu-id="e3453-144">See also</span><span class="sxs-lookup"><span data-stu-id="e3453-144">See also</span></span>
<span data-ttu-id="e3453-145">This document showed you how to implement the Security Center recommendation "Add a Next Generation Firewall."</span><span class="sxs-lookup"><span data-stu-id="e3453-145">This document showed you how to implement the Security Center recommendation "Add a Next Generation Firewall."</span></span> <span data-ttu-id="e3453-146">To learn more about NGFWs and the Check Point partner solution, see the following:</span><span class="sxs-lookup"><span data-stu-id="e3453-146">To learn more about NGFWs and the Check Point partner solution, see the following:</span></span>

* [<span data-ttu-id="e3453-147">Next-Generation Firewall</span><span class="sxs-lookup"><span data-stu-id="e3453-147">Next-Generation Firewall</span></span>](https://en.wikipedia.org/wiki/Next-Generation_Firewall)
* [<span data-ttu-id="e3453-148">Check Point vSEC</span><span class="sxs-lookup"><span data-stu-id="e3453-148">Check Point vSEC</span></span>](https://azure.microsoft.com/marketplace/partners/checkpoint/check-point-r77-10/)

<span data-ttu-id="e3453-149">To learn more about Security Center, see the following:</span><span class="sxs-lookup"><span data-stu-id="e3453-149">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="e3453-150">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies.</span><span class="sxs-lookup"><span data-stu-id="e3453-150">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies.</span></span>
* <span data-ttu-id="e3453-151">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="e3453-151">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="e3453-152">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="e3453-152">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="e3453-153">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span><span class="sxs-lookup"><span data-stu-id="e3453-153">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="e3453-154">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span><span class="sxs-lookup"><span data-stu-id="e3453-154">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="e3453-155">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span><span class="sxs-lookup"><span data-stu-id="e3453-155">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="e3453-156">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span><span class="sxs-lookup"><span data-stu-id="e3453-156">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-add-next-gen-firewall/add-next-gen-firewall.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-add-next-gen-firewall/select-an-endpoint.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-add-next-gen-firewall/create-new-next-gen-firewall.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-add-next-gen-firewall/select-next-gen-firewall.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-add-next-gen-firewall/firewall-solution-info-blade.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-add-next-gen-firewall/create-virtual-machine.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-add-next-gen-firewall/route-traffic-through-ngfw.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-add-next-gen-firewall/select-vm.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-add-next-gen-firewall/configure-rules-to-limit-access.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-add-next-gen-firewall/edit-inbound-rule.png










