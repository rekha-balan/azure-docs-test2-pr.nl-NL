---
title: Protecting your network in Azure Security Center  | Microsoft Docs
description: This document addresses recommendations in Azure Security Center that help you protect your Azure network and stay in compliance with security policies.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: ''
ms.assetid: 96c55a02-afd6-478b-9c1f-039528f3dea0
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2016
ms.author: terrylan
ms.openlocfilehash: 00b715507a7c3a4d784b800e7bf0c700f6ea6ff1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548752"
---
# <a name="protecting-your-network-in-azure-security-center"></a><span data-ttu-id="fda23-103">Protecting your network in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="fda23-103">Protecting your network in Azure Security Center</span></span>
<span data-ttu-id="fda23-104">Azure Security Center analyzes the security state of your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="fda23-104">Azure Security Center analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="fda23-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through the process of configuring the needed controls.</span><span class="sxs-lookup"><span data-stu-id="fda23-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through the process of configuring the needed controls.</span></span>  <span data-ttu-id="fda23-106">Recommendations apply to Azure resource types: virtual machines (VMs), networking, SQL, and applications.</span><span class="sxs-lookup"><span data-stu-id="fda23-106">Recommendations apply to Azure resource types: virtual machines (VMs), networking, SQL, and applications.</span></span>

<span data-ttu-id="fda23-107">This article addresses recommendations that apply to your network.</span><span class="sxs-lookup"><span data-stu-id="fda23-107">This article addresses recommendations that apply to your network.</span></span>  <span data-ttu-id="fda23-108">Network recommendations center around next generation firewalls, Network Security Groups, configuring inbound traffic rules, and more.</span><span class="sxs-lookup"><span data-stu-id="fda23-108">Network recommendations center around next generation firewalls, Network Security Groups, configuring inbound traffic rules, and more.</span></span>  <span data-ttu-id="fda23-109">Use the table below as a reference to help you understand the available network recommendations and what each one does if you apply it.</span><span class="sxs-lookup"><span data-stu-id="fda23-109">Use the table below as a reference to help you understand the available network recommendations and what each one does if you apply it.</span></span>

## <a name="available-network-recommendations"></a><span data-ttu-id="fda23-110">Available network recommendations</span><span class="sxs-lookup"><span data-stu-id="fda23-110">Available network recommendations</span></span>
| <span data-ttu-id="fda23-111">Recommendation</span><span class="sxs-lookup"><span data-stu-id="fda23-111">Recommendation</span></span> | <span data-ttu-id="fda23-112">Description</span><span class="sxs-lookup"><span data-stu-id="fda23-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="fda23-113">Add a Next Generation Firewall</span><span class="sxs-lookup"><span data-stu-id="fda23-113">Add a Next Generation Firewall</span></span>](security-center-add-next-generation-firewall.md) |<span data-ttu-id="fda23-114">Recommends that you add a Next Generation Firewall (NGFW) from a Microsoft partner to increase your security protections.</span><span class="sxs-lookup"><span data-stu-id="fda23-114">Recommends that you add a Next Generation Firewall (NGFW) from a Microsoft partner to increase your security protections.</span></span> |
| [<span data-ttu-id="fda23-115">Route traffic through NGFW only</span><span class="sxs-lookup"><span data-stu-id="fda23-115">Route traffic through NGFW only</span></span>](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |<span data-ttu-id="fda23-116">Recommends that you configure network security group (NSG) rules that force inbound traffic to your VM through your NGFW.</span><span class="sxs-lookup"><span data-stu-id="fda23-116">Recommends that you configure network security group (NSG) rules that force inbound traffic to your VM through your NGFW.</span></span> |
| [<span data-ttu-id="fda23-117">Enable Network Security Groups on subnets or virtual machines</span><span class="sxs-lookup"><span data-stu-id="fda23-117">Enable Network Security Groups on subnets or virtual machines</span></span>](security-center-enable-network-security-groups.md) |<span data-ttu-id="fda23-118">Recommends that you enable NSGs on subnets or VMs.</span><span class="sxs-lookup"><span data-stu-id="fda23-118">Recommends that you enable NSGs on subnets or VMs.</span></span> |
| [<span data-ttu-id="fda23-119">Restrict access through Internet facing endpoint</span><span class="sxs-lookup"><span data-stu-id="fda23-119">Restrict access through Internet facing endpoint</span></span>](security-center-restrict-access-through-internet-facing-endpoints.md) |<span data-ttu-id="fda23-120">Recommends that you configure inbound traffic rules for NSGs.</span><span class="sxs-lookup"><span data-stu-id="fda23-120">Recommends that you configure inbound traffic rules for NSGs.</span></span> |

## <a name="see-also"></a><span data-ttu-id="fda23-121">See also</span><span class="sxs-lookup"><span data-stu-id="fda23-121">See also</span></span>
<span data-ttu-id="fda23-122">To learn more about recommendations that apply to other Azure resource types, see the following:</span><span class="sxs-lookup"><span data-stu-id="fda23-122">To learn more about recommendations that apply to other Azure resource types, see the following:</span></span>

* [<span data-ttu-id="fda23-123">Protecting your virtual machines in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="fda23-123">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="fda23-124">Protecting your applications in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="fda23-124">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="fda23-125">Protecting your Azure SQL service in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="fda23-125">Protecting your Azure SQL service in Azure Security Center</span></span>](security-center-sql-service-recommendations.md)

<span data-ttu-id="fda23-126">To learn more about Security Center, see the following:</span><span class="sxs-lookup"><span data-stu-id="fda23-126">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="fda23-127">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span><span class="sxs-lookup"><span data-stu-id="fda23-127">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="fda23-128">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span><span class="sxs-lookup"><span data-stu-id="fda23-128">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="fda23-129">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span><span class="sxs-lookup"><span data-stu-id="fda23-129">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
