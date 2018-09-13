---
title: Azure AD Connect Synchronization Service Manager Operations | Microsoft Docs
description: Understand the Operations tab in the Synchronization Service Manager for Azure AD Connect.
services: active-directory
documentationcenter: ''
author: andkjell
manager: femila
editor: ''
ms.assetid: 97a26565-618f-4313-8711-5925eeb47cdc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bf490bf79adcee2cb3ee5c285f0f0fab626f0e10
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551768"
---
# <a name="using-the-sync-service-manager-operations-tab"></a><span data-ttu-id="12fe9-103">Using the Sync Service Manager Operations tab</span><span class="sxs-lookup"><span data-stu-id="12fe9-103">Using the Sync Service Manager Operations tab</span></span>

![Sync Service Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-service-manager-ui/operations.png)

<span data-ttu-id="12fe9-105">The operations tab shows the results from the most recent operations.</span><span class="sxs-lookup"><span data-stu-id="12fe9-105">The operations tab shows the results from the most recent operations.</span></span> <span data-ttu-id="12fe9-106">This tab is key to understand and troubleshoot issues.</span><span class="sxs-lookup"><span data-stu-id="12fe9-106">This tab is key to understand and troubleshoot issues.</span></span>

## <a name="understand-the-information-visible-in-the-operations-tab"></a><span data-ttu-id="12fe9-107">Understand the information visible in the operations tab</span><span class="sxs-lookup"><span data-stu-id="12fe9-107">Understand the information visible in the operations tab</span></span>
<span data-ttu-id="12fe9-108">The top half shows all runs in chronological order.</span><span class="sxs-lookup"><span data-stu-id="12fe9-108">The top half shows all runs in chronological order.</span></span> <span data-ttu-id="12fe9-109">By default, the operations log keeps information about the last seven days, but this setting can be changed with the [scheduler](active-directory-aadconnectsync-feature-scheduler.md).</span><span class="sxs-lookup"><span data-stu-id="12fe9-109">By default, the operations log keeps information about the last seven days, but this setting can be changed with the [scheduler](active-directory-aadconnectsync-feature-scheduler.md).</span></span> <span data-ttu-id="12fe9-110">You want to look for any run that does not show a success status.</span><span class="sxs-lookup"><span data-stu-id="12fe9-110">You want to look for any run that does not show a success status.</span></span> <span data-ttu-id="12fe9-111">You can change the sorting by clicking the headers.</span><span class="sxs-lookup"><span data-stu-id="12fe9-111">You can change the sorting by clicking the headers.</span></span>

<span data-ttu-id="12fe9-112">The **Status** column is the most important information and shows the most severe problem for a run.</span><span class="sxs-lookup"><span data-stu-id="12fe9-112">The **Status** column is the most important information and shows the most severe problem for a run.</span></span> <span data-ttu-id="12fe9-113">Here is a quick summary of the most common statuses in order of priority to investigate (where \* indicate several possible error strings).</span><span class="sxs-lookup"><span data-stu-id="12fe9-113">Here is a quick summary of the most common statuses in order of priority to investigate (where \* indicate several possible error strings).</span></span>

| <span data-ttu-id="12fe9-114">Status</span><span class="sxs-lookup"><span data-stu-id="12fe9-114">Status</span></span> | <span data-ttu-id="12fe9-115">Comment</span><span class="sxs-lookup"><span data-stu-id="12fe9-115">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="12fe9-116">stopped-\*</span><span class="sxs-lookup"><span data-stu-id="12fe9-116">stopped-\*</span></span> |<span data-ttu-id="12fe9-117">The run could not complete.</span><span class="sxs-lookup"><span data-stu-id="12fe9-117">The run could not complete.</span></span> <span data-ttu-id="12fe9-118">For example, if the remote system is down and cannot be contacted.</span><span class="sxs-lookup"><span data-stu-id="12fe9-118">For example, if the remote system is down and cannot be contacted.</span></span> |
| <span data-ttu-id="12fe9-119">stopped-error-limit</span><span class="sxs-lookup"><span data-stu-id="12fe9-119">stopped-error-limit</span></span> |<span data-ttu-id="12fe9-120">There are more than 5,000 errors.</span><span class="sxs-lookup"><span data-stu-id="12fe9-120">There are more than 5,000 errors.</span></span> <span data-ttu-id="12fe9-121">The run was automatically stopped due to the large number of errors.</span><span class="sxs-lookup"><span data-stu-id="12fe9-121">The run was automatically stopped due to the large number of errors.</span></span> |
| <span data-ttu-id="12fe9-122">completed-\*-errors</span><span class="sxs-lookup"><span data-stu-id="12fe9-122">completed-\*-errors</span></span> |<span data-ttu-id="12fe9-123">The run completed, but there are errors (fewer than 5,000) that should be investigated.</span><span class="sxs-lookup"><span data-stu-id="12fe9-123">The run completed, but there are errors (fewer than 5,000) that should be investigated.</span></span> |
| <span data-ttu-id="12fe9-124">completed-\*-warnings</span><span class="sxs-lookup"><span data-stu-id="12fe9-124">completed-\*-warnings</span></span> |<span data-ttu-id="12fe9-125">The run completed, but some data is not in the expected state.</span><span class="sxs-lookup"><span data-stu-id="12fe9-125">The run completed, but some data is not in the expected state.</span></span> <span data-ttu-id="12fe9-126">If you have errors, then this message is usually only a symptom.</span><span class="sxs-lookup"><span data-stu-id="12fe9-126">If you have errors, then this message is usually only a symptom.</span></span> <span data-ttu-id="12fe9-127">Until you have addressed errors, you should not investigate warnings.</span><span class="sxs-lookup"><span data-stu-id="12fe9-127">Until you have addressed errors, you should not investigate warnings.</span></span> |
| <span data-ttu-id="12fe9-128">success</span><span class="sxs-lookup"><span data-stu-id="12fe9-128">success</span></span> |<span data-ttu-id="12fe9-129">No issues.</span><span class="sxs-lookup"><span data-stu-id="12fe9-129">No issues.</span></span> |

<span data-ttu-id="12fe9-130">When you select a row, the bottom updates to show the details of that run.</span><span class="sxs-lookup"><span data-stu-id="12fe9-130">When you select a row, the bottom updates to show the details of that run.</span></span> <span data-ttu-id="12fe9-131">To the far left of the bottom, you might have a list saying **Step #**.</span><span class="sxs-lookup"><span data-stu-id="12fe9-131">To the far left of the bottom, you might have a list saying **Step #**.</span></span> <span data-ttu-id="12fe9-132">This list only appears if you have multiple domains in your forest where each domain is represented by a step.</span><span class="sxs-lookup"><span data-stu-id="12fe9-132">This list only appears if you have multiple domains in your forest where each domain is represented by a step.</span></span> <span data-ttu-id="12fe9-133">The domain name can be found under the heading **Partition**.</span><span class="sxs-lookup"><span data-stu-id="12fe9-133">The domain name can be found under the heading **Partition**.</span></span> <span data-ttu-id="12fe9-134">Under **Synchronization Statistics**, you can find more information about the number of changes that were processed.</span><span class="sxs-lookup"><span data-stu-id="12fe9-134">Under **Synchronization Statistics**, you can find more information about the number of changes that were processed.</span></span> <span data-ttu-id="12fe9-135">You can click the links to get a list of the changed objects.</span><span class="sxs-lookup"><span data-stu-id="12fe9-135">You can click the links to get a list of the changed objects.</span></span> <span data-ttu-id="12fe9-136">If you have objects with errors, those errors show up under **Synchronization Errors**.</span><span class="sxs-lookup"><span data-stu-id="12fe9-136">If you have objects with errors, those errors show up under **Synchronization Errors**.</span></span>

<span data-ttu-id="12fe9-137">For more information, see [troubleshoot an object that is not synchronizing](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md)</span><span class="sxs-lookup"><span data-stu-id="12fe9-137">For more information, see [troubleshoot an object that is not synchronizing](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="12fe9-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="12fe9-138">Next steps</span></span>
<span data-ttu-id="12fe9-139">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span><span class="sxs-lookup"><span data-stu-id="12fe9-139">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="12fe9-140">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="12fe9-140">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

