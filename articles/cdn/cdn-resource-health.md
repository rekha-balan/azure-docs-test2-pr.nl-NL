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
ms.openlocfilehash: b560eb877c57ebdcc02b7a9457c44a4acff3851e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555481"
---
# <a name="monitor-the-health-of-azure-cdn-resources"></a><span data-ttu-id="b820d-103">Monitor the health of Azure CDN resources</span><span class="sxs-lookup"><span data-stu-id="b820d-103">Monitor the health of Azure CDN resources</span></span>
  
<span data-ttu-id="b820d-104">Azure CDN Resource health is a subset of [Azure resource health](../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b820d-104">Azure CDN Resource health is a subset of [Azure resource health](../resource-health/resource-health-overview.md).</span></span>  <span data-ttu-id="b820d-105">You can use Azure resource health to monitor the health of CDN resources and receive actionable guidance to troubleshoot problems.</span><span class="sxs-lookup"><span data-stu-id="b820d-105">You can use Azure resource health to monitor the health of CDN resources and receive actionable guidance to troubleshoot problems.</span></span>

>[!IMPORTANT] 
><span data-ttu-id="b820d-106">Azure CDN resource health only currently accounts for the health of global CDN delivery and API capabilities.</span><span class="sxs-lookup"><span data-stu-id="b820d-106">Azure CDN resource health only currently accounts for the health of global CDN delivery and API capabilities.</span></span>  <span data-ttu-id="b820d-107">Azure CDN resource health does not verify individual CDN endpoints.</span><span class="sxs-lookup"><span data-stu-id="b820d-107">Azure CDN resource health does not verify individual CDN endpoints.</span></span>
>
><span data-ttu-id="b820d-108">The signals that feed Azure CDN resource health may be up to 15 minutes delayed.</span><span class="sxs-lookup"><span data-stu-id="b820d-108">The signals that feed Azure CDN resource health may be up to 15 minutes delayed.</span></span>

## <a name="how-to-find-azure-cdn-resource-health"></a><span data-ttu-id="b820d-109">How to find Azure CDN resource health</span><span class="sxs-lookup"><span data-stu-id="b820d-109">How to find Azure CDN resource health</span></span>

1. <span data-ttu-id="b820d-110">In the [Azure portal](https://portal.azure.com), browse to your CDN profile.</span><span class="sxs-lookup"><span data-stu-id="b820d-110">In the [Azure portal](https://portal.azure.com), browse to your CDN profile.</span></span>

2. <span data-ttu-id="b820d-111">Click the **Settings** button.</span><span class="sxs-lookup"><span data-stu-id="b820d-111">Click the **Settings** button.</span></span>

    ![Settings button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-resource-health/cdn-profile-settings.png)

3. <span data-ttu-id="b820d-113">Under *Support + troubleshooting*, click **Resource health**.</span><span class="sxs-lookup"><span data-stu-id="b820d-113">Under *Support + troubleshooting*, click **Resource health**.</span></span>

    ![CDN resource health](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-resource-health/cdn-resource-health3.png)

>[!TIP] 
><span data-ttu-id="b820d-115">You can also find CDN resources listed in the *Resource health* tile in the *Help + support* blade.</span><span class="sxs-lookup"><span data-stu-id="b820d-115">You can also find CDN resources listed in the *Resource health* tile in the *Help + support* blade.</span></span>  <span data-ttu-id="b820d-116">You can quickly get to *Help + support* by clicking the circled **?**</span><span class="sxs-lookup"><span data-stu-id="b820d-116">You can quickly get to *Help + support* by clicking the circled **?**</span></span> <span data-ttu-id="b820d-117">in the upper right corner of the portal.</span><span class="sxs-lookup"><span data-stu-id="b820d-117">in the upper right corner of the portal.</span></span>
>
> ![Help + support](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-resource-health/cdn-help-support.png)

## <a name="azure-cdn-specific-messages"></a><span data-ttu-id="b820d-119">Azure CDN-specific messages</span><span class="sxs-lookup"><span data-stu-id="b820d-119">Azure CDN-specific messages</span></span>

<span data-ttu-id="b820d-120">Statuses related to Azure CDN resource health can be found below.</span><span class="sxs-lookup"><span data-stu-id="b820d-120">Statuses related to Azure CDN resource health can be found below.</span></span>

|<span data-ttu-id="b820d-121">Message</span><span class="sxs-lookup"><span data-stu-id="b820d-121">Message</span></span> | <span data-ttu-id="b820d-122">Recommended Action</span><span class="sxs-lookup"><span data-stu-id="b820d-122">Recommended Action</span></span> |
|---|---|
|<span data-ttu-id="b820d-123">You may have stopped, removed, or misconfigured one or more of your CDN endpoints</span><span class="sxs-lookup"><span data-stu-id="b820d-123">You may have stopped, removed, or misconfigured one or more of your CDN endpoints</span></span> | <span data-ttu-id="b820d-124">You may have stopped, removed, or misconfigured one or more of your CDN endpoints.</span><span class="sxs-lookup"><span data-stu-id="b820d-124">You may have stopped, removed, or misconfigured one or more of your CDN endpoints.</span></span>|
|<span data-ttu-id="b820d-125">We are sorry, the CDN management service is currently unavailable</span><span class="sxs-lookup"><span data-stu-id="b820d-125">We are sorry, the CDN management service is currently unavailable</span></span> | <span data-ttu-id="b820d-126">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span><span class="sxs-lookup"><span data-stu-id="b820d-126">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span>|
|<span data-ttu-id="b820d-127">We're sorry, your CDN endpoints may be impacted by ongoing issues with some of our CDN providers</span><span class="sxs-lookup"><span data-stu-id="b820d-127">We're sorry, your CDN endpoints may be impacted by ongoing issues with some of our CDN providers</span></span> | <span data-ttu-id="b820d-128">Check back here for status updates; Use the Troubleshoot tool to learn how to test your origin and CDN endpoint; If your problem persists after the expected resolution time, contact support.</span><span class="sxs-lookup"><span data-stu-id="b820d-128">Check back here for status updates; Use the Troubleshoot tool to learn how to test your origin and CDN endpoint; If your problem persists after the expected resolution time, contact support.</span></span> |
|<span data-ttu-id="b820d-129">We're sorry, CDN endpoint configuration changes are experiencing propagation delays</span><span class="sxs-lookup"><span data-stu-id="b820d-129">We're sorry, CDN endpoint configuration changes are experiencing propagation delays</span></span> | <span data-ttu-id="b820d-130">Check back here for status updates; If your configuration changes are not fully propagated in the expected time, contact support.</span><span class="sxs-lookup"><span data-stu-id="b820d-130">Check back here for status updates; If your configuration changes are not fully propagated in the expected time, contact support.</span></span>|
|<span data-ttu-id="b820d-131">We're sorry, we are experiencing issues loading the supplemental portal</span><span class="sxs-lookup"><span data-stu-id="b820d-131">We're sorry, we are experiencing issues loading the supplemental portal</span></span> | <span data-ttu-id="b820d-132">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span><span class="sxs-lookup"><span data-stu-id="b820d-132">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span>|
<span data-ttu-id="b820d-133">We are sorry, we are experiencing issues with some of our CDN providers</span><span class="sxs-lookup"><span data-stu-id="b820d-133">We are sorry, we are experiencing issues with some of our CDN providers</span></span> | <span data-ttu-id="b820d-134">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span><span class="sxs-lookup"><span data-stu-id="b820d-134">Check back here for status updates; If your problem persists after the expected resolution time, contact support.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b820d-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="b820d-135">Next steps</span></span>

- [<span data-ttu-id="b820d-136">Read an overview of Azure resource health</span><span class="sxs-lookup"><span data-stu-id="b820d-136">Read an overview of Azure resource health</span></span>](../resource-health/resource-health-overview.md)
- [<span data-ttu-id="b820d-137">Troubleshoot issues with CDN compression</span><span class="sxs-lookup"><span data-stu-id="b820d-137">Troubleshoot issues with CDN compression</span></span>](./cdn-troubleshoot-compression.md)
- [<span data-ttu-id="b820d-138">Troubleshoot issues with 404 errors</span><span class="sxs-lookup"><span data-stu-id="b820d-138">Troubleshoot issues with 404 errors</span></span>](./cdn-troubleshoot-endpoint.md)


