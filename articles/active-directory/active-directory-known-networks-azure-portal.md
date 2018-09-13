---
title: Named networks in Azure Active Directory | Microsoft Docs
description: By configuring named networks, you can avoid having IP addresses that are owned by your organization generate the creation of false positives for the sign ins from multiple geographies and sign ins from IP addresses with suspicious activity risk events.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: femila
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/06/2017
ms.author: markvi
ms.openlocfilehash: 1dac341c4dc0b7c93791f91d8783c434f3c5d745
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554780"
---
# <a name="named-networks-in-azure-active-directory"></a><span data-ttu-id="9d715-103">Named networks in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9d715-103">Named networks in Azure Active Directory</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](active-directory-known-networks-azure-portal.md)
> * [Azure classic portal](active-directory-known-networks.md)
>
>


<span data-ttu-id="9d715-106">Azure Active Directory creates a record for each detected [risk event](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="9d715-106">Azure Active Directory creates a record for each detected [risk event](active-directory-identity-protection-risk-events.md).</span></span> <span data-ttu-id="9d715-107">With the risk event information available through the Azure Active Directory security reports, you can gain insights into the probability of compromised user accounts in your environment.</span><span class="sxs-lookup"><span data-stu-id="9d715-107">With the risk event information available through the Azure Active Directory security reports, you can gain insights into the probability of compromised user accounts in your environment.</span></span>   

<span data-ttu-id="9d715-108">It is possible that Azure Active Directory detects false positives of the *impossible travel to atypical locations* and the *sign ins from IP addresses with suspicious activity* [risk event types](active-directory-reporting-risk-events.md#risk-event-types) for IP addresses that are actually owned by your organization.</span><span class="sxs-lookup"><span data-stu-id="9d715-108">It is possible that Azure Active Directory detects false positives of the *impossible travel to atypical locations* and the *sign ins from IP addresses with suspicious activity* [risk event types](active-directory-reporting-risk-events.md#risk-event-types) for IP addresses that are actually owned by your organization.</span></span> 

<span data-ttu-id="9d715-109">This can, for example, happen when:</span><span class="sxs-lookup"><span data-stu-id="9d715-109">This can, for example, happen when:</span></span>

- <span data-ttu-id="9d715-110">A user in your Boston office has signed in remotely to your data center in San Francisco generates a *sign ins from multiple geographies* risk event</span><span class="sxs-lookup"><span data-stu-id="9d715-110">A user in your Boston office has signed in remotely to your data center in San Francisco generates a *sign ins from multiple geographies* risk event</span></span>

- <span data-ttu-id="9d715-111">A user of your organization tries to sign-on several times with an incorrect password generates a *sign ins from IP addresses with suspicious activity* risk event</span><span class="sxs-lookup"><span data-stu-id="9d715-111">A user of your organization tries to sign-on several times with an incorrect password generates a *sign ins from IP addresses with suspicious activity* risk event</span></span>

<span data-ttu-id="9d715-112">To prevent these cases from generating misleading risk events, you should add named IP address ranges to the list of your organization's public IP address.</span><span class="sxs-lookup"><span data-stu-id="9d715-112">To prevent these cases from generating misleading risk events, you should add named IP address ranges to the list of your organization's public IP address.</span></span>    

### <a name="to-add-your-organizations-public-ip-address-ranges-perform-the-following-steps"></a><span data-ttu-id="9d715-113">To add your organization’s public IP address ranges, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9d715-113">To add your organization’s public IP address ranges, perform the following steps:</span></span>

1. <span data-ttu-id="9d715-114">Sign-on to the Azure management portal.</span><span class="sxs-lookup"><span data-stu-id="9d715-114">Sign-on to the Azure management portal.</span></span>

2. <span data-ttu-id="9d715-115">In the left pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9d715-115">In the left pane, click **Active Directory**.</span></span>

    ![Known Networks](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-known-networks-azure-portal/01.png)

3. <span data-ttu-id="9d715-117">On the directory blade, in the **Manage** section, click **Named networks**.</span><span class="sxs-lookup"><span data-stu-id="9d715-117">On the directory blade, in the **Manage** section, click **Named networks**.</span></span>

    ![Known Networks](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-known-networks-azure-portal/02.png)


4. <span data-ttu-id="9d715-119">Click **Add location**</span><span class="sxs-lookup"><span data-stu-id="9d715-119">Click **Add location**</span></span>

    ![Known Networks](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-known-networks-azure-portal/03.png)

5. <span data-ttu-id="9d715-121">On the **Add** blade, do:</span><span class="sxs-lookup"><span data-stu-id="9d715-121">On the **Add** blade, do:</span></span>

    ![Known Networks](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-known-networks-azure-portal/04.png)

    <span data-ttu-id="9d715-123">a.</span><span class="sxs-lookup"><span data-stu-id="9d715-123">a.</span></span> <span data-ttu-id="9d715-124">In the **Name** textbox, type a name.</span><span class="sxs-lookup"><span data-stu-id="9d715-124">In the **Name** textbox, type a name.</span></span>

    <span data-ttu-id="9d715-125">b.</span><span class="sxs-lookup"><span data-stu-id="9d715-125">b.</span></span> <span data-ttu-id="9d715-126">In the **IP range** textbox, type an IP range.</span><span class="sxs-lookup"><span data-stu-id="9d715-126">In the **IP range** textbox, type an IP range.</span></span> <span data-ttu-id="9d715-127">The IP range needs to be in CIDR format.</span><span class="sxs-lookup"><span data-stu-id="9d715-127">The IP range needs to be in CIDR format.</span></span> <span data-ttu-id="9d715-128">For bulk update, you can upload a CSV file with the IP ranges.</span><span class="sxs-lookup"><span data-stu-id="9d715-128">For bulk update, you can upload a CSV file with the IP ranges.</span></span> <span data-ttu-id="9d715-129">An upload adds the IP ranges in the file to the list instead of overwriting the list.</span><span class="sxs-lookup"><span data-stu-id="9d715-129">An upload adds the IP ranges in the file to the list instead of overwriting the list.</span></span>

    <span data-ttu-id="9d715-130">c.</span><span class="sxs-lookup"><span data-stu-id="9d715-130">c.</span></span> <span data-ttu-id="9d715-131">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="9d715-131">Click **Create**.</span></span>


<span data-ttu-id="9d715-132">**Additional resources:**</span><span class="sxs-lookup"><span data-stu-id="9d715-132">**Additional resources:**</span></span>

* [<span data-ttu-id="9d715-133">View your access and usage reports</span><span class="sxs-lookup"><span data-stu-id="9d715-133">View your access and usage reports</span></span>](active-directory-view-access-usage-reports.md)
* [<span data-ttu-id="9d715-134">Sign ins from IP addresses with suspicious activity</span><span class="sxs-lookup"><span data-stu-id="9d715-134">Sign ins from IP addresses with suspicious activity</span></span>](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md)
* [<span data-ttu-id="9d715-135">Sign ins from multiple geographies</span><span class="sxs-lookup"><span data-stu-id="9d715-135">Sign ins from multiple geographies</span></span>](active-directory-reporting-sign-ins-from-multiple-geographies.md)




