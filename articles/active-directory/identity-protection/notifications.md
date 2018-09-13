---
title: Azure Active Directory Identity Protection notifications| Microsoft Docs
description: Learn how notifications support your investigation activities.
services: active-directory
keywords: azure active directory identity protection, cloud app discovery, managing applications, security, risk, risk level, vulnerability, security policy
documentationcenter: ''
author: MarkusVi
manager: mtillman
editor: ''
ms.assetid: 65ca79b9-4da1-4d5b-bebd-eda776cc32c7
ms.service: active-directory
ms.component: conditional-access
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 0a546acd05246e011fa66abea8a667d0b3513588
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864566"
---
# <a name="azure-active-directory-identity-protection-notifications"></a><span data-ttu-id="b9da7-104">Azure Active Directory Identity Protection notifications</span><span class="sxs-lookup"><span data-stu-id="b9da7-104">Azure Active Directory Identity Protection notifications</span></span>

<span data-ttu-id="b9da7-105">Azure AD Identity Protection sends two types of automated notification emails to help you manage user risk and risk events:</span><span class="sxs-lookup"><span data-stu-id="b9da7-105">Azure AD Identity Protection sends two types of automated notification emails to help you manage user risk and risk events:</span></span>

- <span data-ttu-id="b9da7-106">Users at risk detected email</span><span class="sxs-lookup"><span data-stu-id="b9da7-106">Users at risk detected email</span></span>
- <span data-ttu-id="b9da7-107">Weekly digest email</span><span class="sxs-lookup"><span data-stu-id="b9da7-107">Weekly digest email</span></span>

<span data-ttu-id="b9da7-108">This article provides you with an overview of both notification emails.</span><span class="sxs-lookup"><span data-stu-id="b9da7-108">This article provides you with an overview of both notification emails.</span></span>


## <a name="users-at-risk-detected-email"></a><span data-ttu-id="b9da7-109">Users at risk detected email</span><span class="sxs-lookup"><span data-stu-id="b9da7-109">Users at risk detected email</span></span>

<span data-ttu-id="b9da7-110">In response to a detected account at risk, Azure AD Identity Protection generates an email alert with **Users at risk detected** as subject.</span><span class="sxs-lookup"><span data-stu-id="b9da7-110">In response to a detected account at risk, Azure AD Identity Protection generates an email alert with **Users at risk detected** as subject.</span></span> <span data-ttu-id="b9da7-111">The email includes a link to the **[Users flagged for risk](../reports-monitoring/concept-user-at-risk.md)** report.</span><span class="sxs-lookup"><span data-stu-id="b9da7-111">The email includes a link to the **[Users flagged for risk](../reports-monitoring/concept-user-at-risk.md)** report.</span></span> <span data-ttu-id="b9da7-112">As a best practice, you should immediately investigate the users at risk.</span><span class="sxs-lookup"><span data-stu-id="b9da7-112">As a best practice, you should immediately investigate the users at risk.</span></span>

![Users at risk detected email](./media/notifications/01.png)


### <a name="configuration"></a><span data-ttu-id="b9da7-114">Configuration</span><span class="sxs-lookup"><span data-stu-id="b9da7-114">Configuration</span></span>

<span data-ttu-id="b9da7-115">As an administrator, you can set:</span><span class="sxs-lookup"><span data-stu-id="b9da7-115">As an administrator, you can set:</span></span>

- <span data-ttu-id="b9da7-116">**The risk level that triggers the generation of this email** - By default, the risk level is set to “High” risk.</span><span class="sxs-lookup"><span data-stu-id="b9da7-116">**The risk level that triggers the generation of this email** - By default, the risk level is set to “High” risk.</span></span>
- <span data-ttu-id="b9da7-117">**The recipients of this email** - By default, recipients include all Global Admins.</span><span class="sxs-lookup"><span data-stu-id="b9da7-117">**The recipients of this email** - By default, recipients include all Global Admins.</span></span> <span data-ttu-id="b9da7-118">Global Admins can also add other Global Admins, Security Admins, Security Readers as recipients.</span><span class="sxs-lookup"><span data-stu-id="b9da7-118">Global Admins can also add other Global Admins, Security Admins, Security Readers as recipients.</span></span>  


<span data-ttu-id="b9da7-119">To open the related dialog, click **Alerts** in the **Settings** section of the **Identity Protection** page.</span><span class="sxs-lookup"><span data-stu-id="b9da7-119">To open the related dialog, click **Alerts** in the **Settings** section of the **Identity Protection** page.</span></span>

![Users at risk detected email](./media/notifications/05.png)


## <a name="weekly-digest-email"></a><span data-ttu-id="b9da7-121">Weekly digest email</span><span class="sxs-lookup"><span data-stu-id="b9da7-121">Weekly digest email</span></span>

<span data-ttu-id="b9da7-122">The weekly digest email contains a summary of new risk events.</span><span class="sxs-lookup"><span data-stu-id="b9da7-122">The weekly digest email contains a summary of new risk events.</span></span>  
<span data-ttu-id="b9da7-123">It includes:</span><span class="sxs-lookup"><span data-stu-id="b9da7-123">It includes:</span></span>

- <span data-ttu-id="b9da7-124">Users at risk</span><span class="sxs-lookup"><span data-stu-id="b9da7-124">Users at risk</span></span>

- <span data-ttu-id="b9da7-125">Suspicious activities</span><span class="sxs-lookup"><span data-stu-id="b9da7-125">Suspicious activities</span></span>

- <span data-ttu-id="b9da7-126">Detected vulnerabilities</span><span class="sxs-lookup"><span data-stu-id="b9da7-126">Detected vulnerabilities</span></span>

- <span data-ttu-id="b9da7-127">Links to the related reports in Identity Protection</span><span class="sxs-lookup"><span data-stu-id="b9da7-127">Links to the related reports in Identity Protection</span></span>

    <span data-ttu-id="b9da7-128">![Remediation](./media/notifications/400.png "Remediation")</span><span class="sxs-lookup"><span data-stu-id="b9da7-128">![Remediation](./media/notifications/400.png "Remediation")</span></span>

### <a name="configuration"></a><span data-ttu-id="b9da7-129">Configuration</span><span class="sxs-lookup"><span data-stu-id="b9da7-129">Configuration</span></span>

<span data-ttu-id="b9da7-130">As an administrator, you can switch sending a weekly digest email off.</span><span class="sxs-lookup"><span data-stu-id="b9da7-130">As an administrator, you can switch sending a weekly digest email off.</span></span>

<span data-ttu-id="b9da7-131">![User risks](./media/notifications/62.png "User risks")</span><span class="sxs-lookup"><span data-stu-id="b9da7-131">![User risks](./media/notifications/62.png "User risks")</span></span>

<span data-ttu-id="b9da7-132">To open the related dialog, click **Weekly Digest** in the **Settings** section of the **Identity Protection** page.</span><span class="sxs-lookup"><span data-stu-id="b9da7-132">To open the related dialog, click **Weekly Digest** in the **Settings** section of the **Identity Protection** page.</span></span>

![Users at risk detected email](./media/notifications/04.png)


## <a name="see-also"></a><span data-ttu-id="b9da7-134">See also</span><span class="sxs-lookup"><span data-stu-id="b9da7-134">See also</span></span>

- [<span data-ttu-id="b9da7-135">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="b9da7-135">Azure Active Directory Identity Protection</span></span>](../active-directory-identityprotection.md)
