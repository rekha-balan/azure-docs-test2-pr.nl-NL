---
title: Enable Network Security Groups in Azure Security Center | Microsoft Docs
description: This document shows you how to implement the Azure Security Center recommendation **Enable Network Security Groups**.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: ''
ms.assetid: f53ed853-ffaf-4530-a019-1906ba6f341b
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: ea3a83573f50c647ec8042961d2b5e371ebef029
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671822"
---
# <a name="enable-network-security-groups-in-azure-security-center"></a><span data-ttu-id="8224f-103">Enable Network Security Groups in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="8224f-103">Enable Network Security Groups in Azure Security Center</span></span>
<span data-ttu-id="8224f-104">Azure Security Center recommends that you enable a network security group (NSG) if one is not already enabled.</span><span class="sxs-lookup"><span data-stu-id="8224f-104">Azure Security Center recommends that you enable a network security group (NSG) if one is not already enabled.</span></span> <span data-ttu-id="8224f-105">NSGs contain a list of Access Control List (ACL) rules that allow or deny network traffic to your VM instances in a Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="8224f-105">NSGs contain a list of Access Control List (ACL) rules that allow or deny network traffic to your VM instances in a Virtual Network.</span></span> <span data-ttu-id="8224f-106">NSGs can be associated with either subnets or individual VM instances within that subnet.</span><span class="sxs-lookup"><span data-stu-id="8224f-106">NSGs can be associated with either subnets or individual VM instances within that subnet.</span></span> <span data-ttu-id="8224f-107">When an NSG is associated with a subnet, the ACL rules apply to all the VM instances in that subnet.</span><span class="sxs-lookup"><span data-stu-id="8224f-107">When an NSG is associated with a subnet, the ACL rules apply to all the VM instances in that subnet.</span></span> <span data-ttu-id="8224f-108">In addition, traffic to an individual VM can be restricted further by associating an NSG directly to that VM.</span><span class="sxs-lookup"><span data-stu-id="8224f-108">In addition, traffic to an individual VM can be restricted further by associating an NSG directly to that VM.</span></span> <span data-ttu-id="8224f-109">To learn more see [What is a Network Security Group (NSG)?](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="8224f-109">To learn more see [What is a Network Security Group (NSG)?](../virtual-network/virtual-networks-nsg.md)</span></span>

<span data-ttu-id="8224f-110">If you do not have NSGs enabled, Security Center presents two recommendations to you: Enable Network Security Groups on subnets and Enable Network Security Groups on virtual machines.</span><span class="sxs-lookup"><span data-stu-id="8224f-110">If you do not have NSGs enabled, Security Center presents two recommendations to you: Enable Network Security Groups on subnets and Enable Network Security Groups on virtual machines.</span></span> <span data-ttu-id="8224f-111">You choose which level, subnet or VM, to apply NSGs.</span><span class="sxs-lookup"><span data-stu-id="8224f-111">You choose which level, subnet or VM, to apply NSGs.</span></span>

> [!NOTE]
> <span data-ttu-id="8224f-112">This document introduces the service by using an example deployment.</span><span class="sxs-lookup"><span data-stu-id="8224f-112">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="8224f-113">This is not a step-by-step guide.</span><span class="sxs-lookup"><span data-stu-id="8224f-113">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="8224f-114">Implement the recommendation</span><span class="sxs-lookup"><span data-stu-id="8224f-114">Implement the recommendation</span></span>
1. <span data-ttu-id="8224f-115">In the **Recommendations** blade, select **Enable Network Security Groups** on subnets or on virtual machines.</span><span class="sxs-lookup"><span data-stu-id="8224f-115">In the **Recommendations** blade, select **Enable Network Security Groups** on subnets or on virtual machines.</span></span>
   <span data-ttu-id="8224f-116">![Enable Network Security Groups][1]</span><span class="sxs-lookup"><span data-stu-id="8224f-116">![Enable Network Security Groups][1]</span></span>
2. <span data-ttu-id="8224f-117">This opens the blade **Configure Missing Network Security Groups** for subnets or for virtual machines, depending on the recommendation that you selected.</span><span class="sxs-lookup"><span data-stu-id="8224f-117">This opens the blade **Configure Missing Network Security Groups** for subnets or for virtual machines, depending on the recommendation that you selected.</span></span> <span data-ttu-id="8224f-118">Select a subnet or a virtual machine to configure an NSG on.</span><span class="sxs-lookup"><span data-stu-id="8224f-118">Select a subnet or a virtual machine to configure an NSG on.</span></span>

   ![Configure NSG for subnet][2]

   ![Configure NSG for VM][3]
3. <span data-ttu-id="8224f-121">On the **Choose network security group** blade, select an existing NSG or select **Create new** to create an NSG.</span><span class="sxs-lookup"><span data-stu-id="8224f-121">On the **Choose network security group** blade, select an existing NSG or select **Create new** to create an NSG.</span></span>

   ![Choose Network Security Group][4]

<span data-ttu-id="8224f-123">If you create an NSG, follow the steps in [How to manage NSGs using the Azure portal](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) to create an NSG and set security rules.</span><span class="sxs-lookup"><span data-stu-id="8224f-123">If you create an NSG, follow the steps in [How to manage NSGs using the Azure portal](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) to create an NSG and set security rules.</span></span>

## <a name="see-also"></a><span data-ttu-id="8224f-124">See also</span><span class="sxs-lookup"><span data-stu-id="8224f-124">See also</span></span>
<span data-ttu-id="8224f-125">This article showed you how to implement the Security Center recommendation "Enable Network Security Groups" for subnets or virtual machines.</span><span class="sxs-lookup"><span data-stu-id="8224f-125">This article showed you how to implement the Security Center recommendation "Enable Network Security Groups" for subnets or virtual machines.</span></span> <span data-ttu-id="8224f-126">To learn more about enabling NSGs, see the following:</span><span class="sxs-lookup"><span data-stu-id="8224f-126">To learn more about enabling NSGs, see the following:</span></span>

* [<span data-ttu-id="8224f-127">What is a Network Security Group (NSG)?</span><span class="sxs-lookup"><span data-stu-id="8224f-127">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="8224f-128">How to manage NSGs using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="8224f-128">How to manage NSGs using the Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="8224f-129">To learn more about Security Center, see the following:</span><span class="sxs-lookup"><span data-stu-id="8224f-129">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="8224f-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span><span class="sxs-lookup"><span data-stu-id="8224f-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="8224f-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="8224f-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="8224f-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="8224f-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="8224f-133">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span><span class="sxs-lookup"><span data-stu-id="8224f-133">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="8224f-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span><span class="sxs-lookup"><span data-stu-id="8224f-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="8224f-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span><span class="sxs-lookup"><span data-stu-id="8224f-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="8224f-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span><span class="sxs-lookup"><span data-stu-id="8224f-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-enable-nsg/enable-nsg.png
[2]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-enable-nsg/configure-nsg-for-subnet.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-enable-nsg/configure-nsg-for-vm.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/security-center/media/security-center-enable-nsg/choose-nsg.png




