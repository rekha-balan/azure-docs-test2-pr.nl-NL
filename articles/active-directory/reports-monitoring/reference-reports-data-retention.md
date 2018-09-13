---
title: Azure Active Directory report retention policies | Microsoft Docs
description: Retention policies on report data in your Azure Active Directory
services: active-directory
documentationcenter: ''
author: priyamohanram
manager: mtillman
editor: ''
ms.assetid: 183e53b0-0647-42e7-8abe-3e9ff424de12
ms.service: active-directory
ms.devlang: ''
ms.topic: reference
ms.tgt_pltfrm: ''
ms.workload: identity
ms.component: report-monitor
ms.date: 05/10/2018
ms.author: priyamo
ms.reviewer: dhanyahk
ms.openlocfilehash: 68028fd1ba116251860e5c370e9e9ce61fd314bb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969494"
---
# <a name="azure-active-directory-report-retention-policies"></a><span data-ttu-id="e1195-103">Azure Active Directory report retention policies</span><span class="sxs-lookup"><span data-stu-id="e1195-103">Azure Active Directory report retention policies</span></span>


<span data-ttu-id="e1195-104">This article provides you with answers to the most common questions in conjunction with the data retention for the different activity reports in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e1195-104">This article provides you with answers to the most common questions in conjunction with the data retention for the different activity reports in Azure Active Directory.</span></span> 

### <a name="q-how-can-you-get-the-collection-of-activity-data-started"></a><span data-ttu-id="e1195-105">Q: How can you get the collection of activity data started?</span><span class="sxs-lookup"><span data-stu-id="e1195-105">Q: How can you get the collection of activity data started?</span></span>

<span data-ttu-id="e1195-106">**A:**</span><span class="sxs-lookup"><span data-stu-id="e1195-106">**A:**</span></span>

| <span data-ttu-id="e1195-107">Azure AD Edition</span><span class="sxs-lookup"><span data-stu-id="e1195-107">Azure AD Edition</span></span> | <span data-ttu-id="e1195-108">Collection Start</span><span class="sxs-lookup"><span data-stu-id="e1195-108">Collection Start</span></span> |
| :--              | :--   |
| <span data-ttu-id="e1195-109">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="e1195-109">Azure AD Premium P1</span></span> <br /> <span data-ttu-id="e1195-110">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="e1195-110">Azure AD Premium P2</span></span> | <span data-ttu-id="e1195-111">When you sign up for a subscription</span><span class="sxs-lookup"><span data-stu-id="e1195-111">When you sign up for a subscription</span></span> |
| <span data-ttu-id="e1195-112">Azure AD Free</span><span class="sxs-lookup"><span data-stu-id="e1195-112">Azure AD Free</span></span> | <span data-ttu-id="e1195-113">The first time you open the [Azure Active Directory blade](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) or use the [reporting APIs](https://aka.ms/aadreports)</span><span class="sxs-lookup"><span data-stu-id="e1195-113">The first time you open the [Azure Active Directory blade](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) or use the [reporting APIs](https://aka.ms/aadreports)</span></span>  |

---
### <a name="q-when-is-your-activity-data-available-in-the-azure-portal"></a><span data-ttu-id="e1195-114">Q: When is your activity data available in the Azure portal?</span><span class="sxs-lookup"><span data-stu-id="e1195-114">Q: When is your activity data available in the Azure portal?</span></span>

<span data-ttu-id="e1195-115">**A:**</span><span class="sxs-lookup"><span data-stu-id="e1195-115">**A:**</span></span>

- <span data-ttu-id="e1195-116">**Immediately** - If you have already been working with reports in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e1195-116">**Immediately** - If you have already been working with reports in the Azure portal.</span></span>
- <span data-ttu-id="e1195-117">**Within 2 hours** - If you haven’t turned on reporting in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e1195-117">**Within 2 hours** - If you haven’t turned on reporting in the Azure portal.</span></span>

---

### <a name="q-how-can-you-get-the-collection-of-security-signals-started"></a><span data-ttu-id="e1195-118">Q: How can you get the collection of security signals started?</span><span class="sxs-lookup"><span data-stu-id="e1195-118">Q: How can you get the collection of security signals started?</span></span>  

<span data-ttu-id="e1195-119">**A:** For security signals, the collection process starts when you opt-in to use the Identity Protection Center.</span><span class="sxs-lookup"><span data-stu-id="e1195-119">**A:** For security signals, the collection process starts when you opt-in to use the Identity Protection Center.</span></span> 


---

### <a name="q-for-how-long-is-the-collected-data-stored"></a><span data-ttu-id="e1195-120">Q: For how long is the collected data stored?</span><span class="sxs-lookup"><span data-stu-id="e1195-120">Q: For how long is the collected data stored?</span></span>

<span data-ttu-id="e1195-121">**A:**</span><span class="sxs-lookup"><span data-stu-id="e1195-121">**A:**</span></span>

<span data-ttu-id="e1195-122">**Activity reports**</span><span class="sxs-lookup"><span data-stu-id="e1195-122">**Activity reports**</span></span>    

| <span data-ttu-id="e1195-123">Report</span><span class="sxs-lookup"><span data-stu-id="e1195-123">Report</span></span>                 | <span data-ttu-id="e1195-124">Azure AD Free</span><span class="sxs-lookup"><span data-stu-id="e1195-124">Azure AD Free</span></span> | <span data-ttu-id="e1195-125">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="e1195-125">Azure AD Premium P1</span></span> | <span data-ttu-id="e1195-126">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="e1195-126">Azure AD Premium P2</span></span> |
| :--                    | :--           | :--                 | :--                 |
| <span data-ttu-id="e1195-127">Directory Audit</span><span class="sxs-lookup"><span data-stu-id="e1195-127">Directory Audit</span></span>        | <span data-ttu-id="e1195-128">7 days</span><span class="sxs-lookup"><span data-stu-id="e1195-128">7 days</span></span>        | <span data-ttu-id="e1195-129">30 days</span><span class="sxs-lookup"><span data-stu-id="e1195-129">30 days</span></span>             | <span data-ttu-id="e1195-130">30 days</span><span class="sxs-lookup"><span data-stu-id="e1195-130">30 days</span></span>             |
| <span data-ttu-id="e1195-131">Sign-in Activity</span><span class="sxs-lookup"><span data-stu-id="e1195-131">Sign-in Activity</span></span>       | <span data-ttu-id="e1195-132">N/A</span><span class="sxs-lookup"><span data-stu-id="e1195-132">N/A</span></span>           | <span data-ttu-id="e1195-133">30 days</span><span class="sxs-lookup"><span data-stu-id="e1195-133">30 days</span></span>             | <span data-ttu-id="e1195-134">30 days</span><span class="sxs-lookup"><span data-stu-id="e1195-134">30 days</span></span>             |
| <span data-ttu-id="e1195-135">Azure MFA Usage</span><span class="sxs-lookup"><span data-stu-id="e1195-135">Azure MFA Usage</span></span>        | <span data-ttu-id="e1195-136">30 days</span><span class="sxs-lookup"><span data-stu-id="e1195-136">30 days</span></span>       | <span data-ttu-id="e1195-137">30 days</span><span class="sxs-lookup"><span data-stu-id="e1195-137">30 days</span></span>             | <span data-ttu-id="e1195-138">30 days</span><span class="sxs-lookup"><span data-stu-id="e1195-138">30 days</span></span>             |

<span data-ttu-id="e1195-139">**Security signals**</span><span class="sxs-lookup"><span data-stu-id="e1195-139">**Security signals**</span></span>

| <span data-ttu-id="e1195-140">Report</span><span class="sxs-lookup"><span data-stu-id="e1195-140">Report</span></span>         | <span data-ttu-id="e1195-141">Azure AD Free</span><span class="sxs-lookup"><span data-stu-id="e1195-141">Azure AD Free</span></span> | <span data-ttu-id="e1195-142">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="e1195-142">Azure AD Premium P1</span></span> | <span data-ttu-id="e1195-143">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="e1195-143">Azure AD Premium P2</span></span> |
| :--            | :--           | :--                 | :--                 |
| <span data-ttu-id="e1195-144">Users at risk</span><span class="sxs-lookup"><span data-stu-id="e1195-144">Users at risk</span></span>  | <span data-ttu-id="e1195-145">7 days</span><span class="sxs-lookup"><span data-stu-id="e1195-145">7 days</span></span>        | <span data-ttu-id="e1195-146">30 days</span><span class="sxs-lookup"><span data-stu-id="e1195-146">30 days</span></span>             | <span data-ttu-id="e1195-147">90 days</span><span class="sxs-lookup"><span data-stu-id="e1195-147">90 days</span></span>             |
| <span data-ttu-id="e1195-148">Risky sign-ins</span><span class="sxs-lookup"><span data-stu-id="e1195-148">Risky sign-ins</span></span> | <span data-ttu-id="e1195-149">7 days</span><span class="sxs-lookup"><span data-stu-id="e1195-149">7 days</span></span>        | <span data-ttu-id="e1195-150">30 days</span><span class="sxs-lookup"><span data-stu-id="e1195-150">30 days</span></span>             | <span data-ttu-id="e1195-151">90 days</span><span class="sxs-lookup"><span data-stu-id="e1195-151">90 days</span></span>             |

---
