---
title: Monitor the health of Azure CDN resources| Microsoft Docs
description: Learn how to monitor the health of your Azure CDN resources using Azure Resource Health.
services: cdn
documentationcenter: .net
author: zhangmanling
manager: zhangmanling
editor: ''
ms.assetid: bf23bd89-35b2-4aca-ac7f-68ee02953f31
ms.service: cdn
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 37fe208f5087f318e665e76825127854b4a11c98
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44811368"
---
# <a name="monitor-the-health-of-azure-cdn-resources"></a><span data-ttu-id="c1243-103">Monitor the health of Azure CDN resources</span><span class="sxs-lookup"><span data-stu-id="c1243-103">Monitor the health of Azure CDN resources</span></span>
  
<span data-ttu-id="c1243-104">Azure CDN Resource health is a subset of [Azure resource health](../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c1243-104">Azure CDN Resource health is a subset of [Azure resource health](../resource-health/resource-health-overview.md).</span></span>  <span data-ttu-id="c1243-105">You can use Azure resource health to monitor the health of CDN resources and receive actionable guidance to troubleshoot problems.</span><span class="sxs-lookup"><span data-stu-id="c1243-105">You can use Azure resource health to monitor the health of CDN resources and receive actionable guidance to troubleshoot problems.</span></span>

>[!IMPORTANT] 
><span data-ttu-id="c1243-106">Azure CDN resource health only currently accounts for the health of global CDN delivery and API capabilities.</span><span class="sxs-lookup"><span data-stu-id="c1243-106">Azure CDN resource health only currently accounts for the health of global CDN delivery and API capabilities.</span></span>  <span data-ttu-id="c1243-107">Azure CDN resource health does not verify individual CDN endpoints.</span><span class="sxs-lookup"><span data-stu-id="c1243-107">Azure CDN resource health does not verify individual CDN endpoints.</span></span>
>
><span data-ttu-id="c1243-108">The signals that feed Azure CDN resource health may be up to 15 minutes delayed.</span><span class="sxs-lookup"><span data-stu-id="c1243-108">The signals that feed Azure CDN resource health may be up to 15 minutes delayed.</span></span>

## <a name="how-to-find-azure-cdn-resource-health"></a><span data-ttu-id="c1243-109">How to find Azure CDN resource health</span><span class="sxs-lookup"><span data-stu-id="c1243-109">How to find Azure CDN resource health</span></span>

1. <span data-ttu-id="c1243-110">In the [Azure portal](https://portal.azure.com), browse to your CDN profile.</span><span class="sxs-lookup"><span data-stu-id="c1243-110">In the [Azure portal](https://portal.azure.com), browse to your CDN profile.</span></span>

2. <span data-ttu-id="c1243-111">Click the **Settings** button.</span><span class="sxs-lookup"><span data-stu-id="c1243-111">Click the **Settings** button.</span></span>

    ![Settings button](./media/cdn-resource-health/cdn-profile-settings.png)

3. <span data-ttu-id="c1243-113">Under *Support + troubleshooting*, click **Resource health**.</span><span class="sxs-lookup"><span data-stu-id="c1243-113">Under *Support + troubleshooting*, click **Resource health**.</span></span>

    ![CDN resource health](./media/cdn-resource-health/cdn-resource-health3.png)

>[!TIP] 
><span data-ttu-id="c1243-115">You can also find CDN resources listed in the *Resource health* tile in the *Help + support* blade.</span><span class="sxs-lookup"><span data-stu-id="c1243-115">You can also find CDN resources listed in the *Resource health* tile in the *Help + support* blade.</span></span>  <span data-ttu-id="c1243-116">You can quickly get to *Help + support* by clicking the circled **?**</span><span class="sxs-lookup"><span data-stu-id="c1243-116">You can quickly get to *Help + support* by clicking the circled **?**</span></span> <span data-ttu-id="c1243-117">in the upper right corner of the portal.</span><span class="sxs-lookup"><span data-stu-id="c1243-117">in the upper right corner of the portal.</span></span>
>
> ![Help + support](./media/cdn-resource-health/cdn-help-support.png)

## <a name="azure-cdn-specific-messages"></a><span data-ttu-id="c1243-119">Azure CDN-specific messages</span><span class="sxs-lookup"><span data-stu-id="c1243-119">Azure CDN-specific messages</span></span>

<span data-ttu-id="c1243-120">Statuses related to Azure CDN resource health can be found below.</span><span class="sxs-lookup"><span data-stu-id="c1243-120">Statuses related to Azure CDN resource health can be found below.</span></span>

|<span data-ttu-id="c1243-121">Message</span><span class="sxs-lookup"><span data-stu-id="c1243-121">Message</span></span> | <span data-ttu-id="c1243-122">Recommended Action</span><span class="sxs-lookup"><span data-stu-id="c1243-122">Recommended Action</span></span> |
|---|---|
|<span data-ttu-id="c1243-123">You may have stopped, removed, or misconfigured one or more of your CDN endpoints</span><span class="sxs-lookup"><span data-stu-id="c1243-123">You may have stopped, removed, or misconfigured one or more of your CDN endpoints</span></span> | <span data-ttu-id="c1243-124">You may have stopped, removed, or misconfigured one or more of your CDN endpoints.</span><span class="sxs-lookup"><span data-stu-id="c1243-124">You may have stopped, removed, or misconfigured one or more of your CDN endpoints.</span></span>|
|<span data-ttu-id="c1243-125">We are sorry, the CDN management service is currently unavailable</span><span class="sxs-lookup"><span data-stu-id="c1243-125">We are sorry, the CDN management service is currently unavailable</span></span> | <span data-ttu-id="c1243-126">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span><span class="sxs-lookup"><span data-stu-id="c1243-126">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span>|
|<span data-ttu-id="c1243-127">We're sorry, your CDN endpoints may be impacted by ongoing issues with some of our CDN providers</span><span class="sxs-lookup"><span data-stu-id="c1243-127">We're sorry, your CDN endpoints may be impacted by ongoing issues with some of our CDN providers</span></span> | <span data-ttu-id="c1243-128">Check back here for status updates; Use the Troubleshoot tool to learn how to test your origin and CDN endpoint; If your problem persists after the expected resolution time, contact support.</span><span class="sxs-lookup"><span data-stu-id="c1243-128">Check back here for status updates; Use the Troubleshoot tool to learn how to test your origin and CDN endpoint; If your problem persists after the expected resolution time, contact support.</span></span> |
|<span data-ttu-id="c1243-129">We're sorry, CDN endpoint configuration changes are experiencing propagation delays</span><span class="sxs-lookup"><span data-stu-id="c1243-129">We're sorry, CDN endpoint configuration changes are experiencing propagation delays</span></span> | <span data-ttu-id="c1243-130">Check back here for status updates; If your configuration changes are not fully propagated in the expected time, contact support.</span><span class="sxs-lookup"><span data-stu-id="c1243-130">Check back here for status updates; If your configuration changes are not fully propagated in the expected time, contact support.</span></span>|
|<span data-ttu-id="c1243-131">We're sorry, we are experiencing issues loading the supplemental portal</span><span class="sxs-lookup"><span data-stu-id="c1243-131">We're sorry, we are experiencing issues loading the supplemental portal</span></span> | <span data-ttu-id="c1243-132">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span><span class="sxs-lookup"><span data-stu-id="c1243-132">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span>|
<span data-ttu-id="c1243-133">We are sorry, we are experiencing issues with some of our CDN providers</span><span class="sxs-lookup"><span data-stu-id="c1243-133">We are sorry, we are experiencing issues with some of our CDN providers</span></span> | <span data-ttu-id="c1243-134">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span><span class="sxs-lookup"><span data-stu-id="c1243-134">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c1243-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="c1243-135">Next steps</span></span>

- [<span data-ttu-id="c1243-136">Read an overview of Azure resource health</span><span class="sxs-lookup"><span data-stu-id="c1243-136">Read an overview of Azure resource health</span></span>](../resource-health/resource-health-overview.md)
- [<span data-ttu-id="c1243-137">Troubleshoot issues with CDN compression</span><span class="sxs-lookup"><span data-stu-id="c1243-137">Troubleshoot issues with CDN compression</span></span>](./cdn-troubleshoot-compression.md)
- [<span data-ttu-id="c1243-138">Troubleshoot issues with 404 errors</span><span class="sxs-lookup"><span data-stu-id="c1243-138">Troubleshoot issues with 404 errors</span></span>](./cdn-troubleshoot-endpoint.md)