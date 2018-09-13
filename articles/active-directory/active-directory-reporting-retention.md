---
title: Azure Active Directory report retention policies | Microsoft Docs
description: Retention policies on report data in your Azure Active Directory
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: femila
editor: ''
ms.assetid: 183e53b0-0647-42e7-8abe-3e9ff424de12
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/06/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: aa7a69c933abfda3bf4d1ac1a298c4ba684efd7e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553747"
---
# <a name="azure-active-directory-report-retention-policies"></a><span data-ttu-id="e0520-103">Azure Active Directory report retention policies</span><span class="sxs-lookup"><span data-stu-id="e0520-103">Azure Active Directory report retention policies</span></span>


<span data-ttu-id="e0520-104">This topic provides you with answers to the most common questions in conjunction with the data retention for the different activity reports in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e0520-104">This topic provides you with answers to the most common questions in conjunction with the data retention for the different activity reports in Azure Active Directory.</span></span> 

<span data-ttu-id="e0520-105">**Q: How can you get the collection of activity data started?**</span><span class="sxs-lookup"><span data-stu-id="e0520-105">**Q: How can you get the collection of activity data started?**</span></span>

<span data-ttu-id="e0520-106">**A:**</span><span class="sxs-lookup"><span data-stu-id="e0520-106">**A:**</span></span>

| <span data-ttu-id="e0520-107">Azure AD Edition</span><span class="sxs-lookup"><span data-stu-id="e0520-107">Azure AD Edition</span></span> | <span data-ttu-id="e0520-108">Collection Start</span><span class="sxs-lookup"><span data-stu-id="e0520-108">Collection Start</span></span> |
| :--              | :--   |
| <span data-ttu-id="e0520-109">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="e0520-109">Azure AD Premium P1</span></span> <br /> <span data-ttu-id="e0520-110">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="e0520-110">Azure AD Premium P2</span></span> | <span data-ttu-id="e0520-111">When you sign-up for a subscription</span><span class="sxs-lookup"><span data-stu-id="e0520-111">When you sign-up for a subscription</span></span> |
| <span data-ttu-id="e0520-112">Azure AD Free</span><span class="sxs-lookup"><span data-stu-id="e0520-112">Azure AD Free</span></span> | <span data-ttu-id="e0520-113">The first time you open the [Azure Active Directory blade](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) or use the [reporting APIs](https://aka.ms/aadreports)</span><span class="sxs-lookup"><span data-stu-id="e0520-113">The first time you open the [Azure Active Directory blade](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) or use the [reporting APIs](https://aka.ms/aadreports)</span></span>  |

---
<span data-ttu-id="e0520-114">**Q: When is your activity data available in the Azure portal?**</span><span class="sxs-lookup"><span data-stu-id="e0520-114">**Q: When is your activity data available in the Azure portal?**</span></span>

<span data-ttu-id="e0520-115">**A:**</span><span class="sxs-lookup"><span data-stu-id="e0520-115">**A:**</span></span>

- <span data-ttu-id="e0520-116">**Immediately** - If you have already been working with reports in the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="e0520-116">**Immediately** - If you have already been working with reports in the Azure classic portal</span></span>
- <span data-ttu-id="e0520-117">**Within 2 hours** - If you haven’t turned reporting on  in the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="e0520-117">**Within 2 hours** - If you haven’t turned reporting on  in the Azure classic portal</span></span>

---
<span data-ttu-id="e0520-118">**Q: How can you get the collection of security signals started?**</span><span class="sxs-lookup"><span data-stu-id="e0520-118">**Q: How can you get the collection of security signals started?**</span></span>  

<span data-ttu-id="e0520-119">**A:** For security signals, the collection process starts when you opt-in to use the Identity Protection Center.</span><span class="sxs-lookup"><span data-stu-id="e0520-119">**A:** For security signals, the collection process starts when you opt-in to use the Identity Protection Center.</span></span> 


---
<span data-ttu-id="e0520-120">**Q: For how long is the collected data stored?**</span><span class="sxs-lookup"><span data-stu-id="e0520-120">**Q: For how long is the collected data stored?**</span></span>

<span data-ttu-id="e0520-121">**A:**</span><span class="sxs-lookup"><span data-stu-id="e0520-121">**A:**</span></span>

<span data-ttu-id="e0520-122">**Activity reports**</span><span class="sxs-lookup"><span data-stu-id="e0520-122">**Activity reports**</span></span>    

| <span data-ttu-id="e0520-123">Report</span><span class="sxs-lookup"><span data-stu-id="e0520-123">Report</span></span>                 | <span data-ttu-id="e0520-124">Azure AD Free</span><span class="sxs-lookup"><span data-stu-id="e0520-124">Azure AD Free</span></span> | <span data-ttu-id="e0520-125">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="e0520-125">Azure AD Premium P1</span></span> | <span data-ttu-id="e0520-126">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="e0520-126">Azure AD Premium P2</span></span> |
| :--                    | :--           | :--                 | :--                 |
| <span data-ttu-id="e0520-127">Directory Audit</span><span class="sxs-lookup"><span data-stu-id="e0520-127">Directory Audit</span></span>        | <span data-ttu-id="e0520-128">7 days</span><span class="sxs-lookup"><span data-stu-id="e0520-128">7 days</span></span>        | <span data-ttu-id="e0520-129">30 days</span><span class="sxs-lookup"><span data-stu-id="e0520-129">30 days</span></span>             | <span data-ttu-id="e0520-130">30 days</span><span class="sxs-lookup"><span data-stu-id="e0520-130">30 days</span></span>             |
| <span data-ttu-id="e0520-131">Sign-in Activity</span><span class="sxs-lookup"><span data-stu-id="e0520-131">Sign-in Activity</span></span>       | <span data-ttu-id="e0520-132">7 days</span><span class="sxs-lookup"><span data-stu-id="e0520-132">7 days</span></span>        | <span data-ttu-id="e0520-133">30 days</span><span class="sxs-lookup"><span data-stu-id="e0520-133">30 days</span></span>             | <span data-ttu-id="e0520-134">30 days</span><span class="sxs-lookup"><span data-stu-id="e0520-134">30 days</span></span>             |

<span data-ttu-id="e0520-135">**Security Signals**</span><span class="sxs-lookup"><span data-stu-id="e0520-135">**Security Signals**</span></span>

| <span data-ttu-id="e0520-136">Report</span><span class="sxs-lookup"><span data-stu-id="e0520-136">Report</span></span>         | <span data-ttu-id="e0520-137">Azure AD Free</span><span class="sxs-lookup"><span data-stu-id="e0520-137">Azure AD Free</span></span> | <span data-ttu-id="e0520-138">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="e0520-138">Azure AD Premium P1</span></span> | <span data-ttu-id="e0520-139">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="e0520-139">Azure AD Premium P2</span></span> |
| :--            | :--           | :--                 | :--                 |
| <span data-ttu-id="e0520-140">Users at risk</span><span class="sxs-lookup"><span data-stu-id="e0520-140">Users at risk</span></span>  | <span data-ttu-id="e0520-141">7 days</span><span class="sxs-lookup"><span data-stu-id="e0520-141">7 days</span></span>        | <span data-ttu-id="e0520-142">30 days</span><span class="sxs-lookup"><span data-stu-id="e0520-142">30 days</span></span>             | <span data-ttu-id="e0520-143">90 days</span><span class="sxs-lookup"><span data-stu-id="e0520-143">90 days</span></span>             |
| <span data-ttu-id="e0520-144">Risky sign-ins</span><span class="sxs-lookup"><span data-stu-id="e0520-144">Risky sign-ins</span></span> | <span data-ttu-id="e0520-145">7 days</span><span class="sxs-lookup"><span data-stu-id="e0520-145">7 days</span></span>        | <span data-ttu-id="e0520-146">30 days</span><span class="sxs-lookup"><span data-stu-id="e0520-146">30 days</span></span>             | <span data-ttu-id="e0520-147">90 days</span><span class="sxs-lookup"><span data-stu-id="e0520-147">90 days</span></span>             |

---