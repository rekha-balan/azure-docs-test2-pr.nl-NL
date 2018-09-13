---
title: Subscription requirements to use PIM - Azure | Microsoft Docs
description: Describes the subscription and licensing requirements to use Azure AD Privileged Identity Management (PIM).
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
editor: markwahl-msft
ms.assetid: 34367721-8b42-4fab-a443-a2e55cdbf33d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.component: pim
ms.date: 06/01/2017
ms.author: rolyon
ms.custom: pim
ms.openlocfilehash: 1554895dcba0c09a3a2e19c284a1cd6f0416cfe1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44784945"
---
# <a name="subscription-requirements-to-use-pim"></a><span data-ttu-id="e7fdb-103">Subscription requirements to use PIM</span><span class="sxs-lookup"><span data-stu-id="e7fdb-103">Subscription requirements to use PIM</span></span>

<span data-ttu-id="e7fdb-104">Azure AD Privileged Identity Management is available as part of the Premium P2 edition of Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7fdb-104">Azure AD Privileged Identity Management is available as part of the Premium P2 edition of Azure AD.</span></span> <span data-ttu-id="e7fdb-105">For more information on the other features of P2 and how it compares to Premium P1, see [Azure Active Directory editions](../active-directory-editions.md).</span><span class="sxs-lookup"><span data-stu-id="e7fdb-105">For more information on the other features of P2 and how it compares to Premium P1, see [Azure Active Directory editions](../active-directory-editions.md).</span></span>

>[!NOTE]
<span data-ttu-id="e7fdb-106">When Azure Active Directory (Azure AD) Privileged Identity Management was in preview, there were no license checks for a tenant to try the service.</span><span class="sxs-lookup"><span data-stu-id="e7fdb-106">When Azure Active Directory (Azure AD) Privileged Identity Management was in preview, there were no license checks for a tenant to try the service.</span></span>  <span data-ttu-id="e7fdb-107">Now that Azure AD Privileged Identity Management has reached general availability, a trial or paid subscription must be present for the tenant to continue using Privileged Identity Management after December 2016.</span><span class="sxs-lookup"><span data-stu-id="e7fdb-107">Now that Azure AD Privileged Identity Management has reached general availability, a trial or paid subscription must be present for the tenant to continue using Privileged Identity Management after December 2016.</span></span>
  

## <a name="confirm-your-trial-or-paid-subscription"></a><span data-ttu-id="e7fdb-108">Confirm your trial or paid subscription</span><span class="sxs-lookup"><span data-stu-id="e7fdb-108">Confirm your trial or paid subscription</span></span>

<span data-ttu-id="e7fdb-109">If you're not sure whether your organization has a trial or purchased subscription, then you can check whether there is a subscription in your tenant by using the commands included in Azure Active Directory Module for Windows PowerShell V1.</span><span class="sxs-lookup"><span data-stu-id="e7fdb-109">If you're not sure whether your organization has a trial or purchased subscription, then you can check whether there is a subscription in your tenant by using the commands included in Azure Active Directory Module for Windows PowerShell V1.</span></span> 
1. <span data-ttu-id="e7fdb-110">Open a PowerShell window.</span><span class="sxs-lookup"><span data-stu-id="e7fdb-110">Open a PowerShell window.</span></span>
2. <span data-ttu-id="e7fdb-111">Enter `Connect-MsolService` to authenticate as a user in your tenant.</span><span class="sxs-lookup"><span data-stu-id="e7fdb-111">Enter `Connect-MsolService` to authenticate as a user in your tenant.</span></span>
3. <span data-ttu-id="e7fdb-112">Enter `Get-MsolSubscription | ft SkuPartNumber,IsTrial,Status`.</span><span class="sxs-lookup"><span data-stu-id="e7fdb-112">Enter `Get-MsolSubscription | ft SkuPartNumber,IsTrial,Status`.</span></span>

<span data-ttu-id="e7fdb-113">This command retrieves a list of the subscriptions in your tenant.</span><span class="sxs-lookup"><span data-stu-id="e7fdb-113">This command retrieves a list of the subscriptions in your tenant.</span></span> <span data-ttu-id="e7fdb-114">If there are no lines returned, you will need to obtain an Azure AD Premium P2 trial, purchase an Azure AD Premium P2 subscription or EMS E5 subscription to use Azure AD Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="e7fdb-114">If there are no lines returned, you will need to obtain an Azure AD Premium P2 trial, purchase an Azure AD Premium P2 subscription or EMS E5 subscription to use Azure AD Privileged Identity Management.</span></span>  <span data-ttu-id="e7fdb-115">To get a trial and start using Azure AD Privileged Identity Management, read [Get started with Azure AD Privileged Identity Management](pim-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="e7fdb-115">To get a trial and start using Azure AD Privileged Identity Management, read [Get started with Azure AD Privileged Identity Management](pim-getting-started.md).</span></span>

<span data-ttu-id="e7fdb-116">If this command returns a line in which SkuPartNumber is "AAD_PREMIUM_P2" or "EMSPREMIUM" and IsTrial is "True", this indicates an Azure AD Premium P2 trial is present in the tenant.</span><span class="sxs-lookup"><span data-stu-id="e7fdb-116">If this command returns a line in which SkuPartNumber is "AAD_PREMIUM_P2" or "EMSPREMIUM" and IsTrial is "True", this indicates an Azure AD Premium P2 trial is present in the tenant.</span></span>  <span data-ttu-id="e7fdb-117">If the subscription status is not enabled, and you do not have an Azure AD Premium P2 or EMS E5 subscription purchase, then you must purchase an Azure AD Premium P2 subscription or EMS E5 subscription to continue using Azure AD Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="e7fdb-117">If the subscription status is not enabled, and you do not have an Azure AD Premium P2 or EMS E5 subscription purchase, then you must purchase an Azure AD Premium P2 subscription or EMS E5 subscription to continue using Azure AD Privileged Identity Management.</span></span>

<span data-ttu-id="e7fdb-118">Azure AD Premium P2 is available through a [Microsoft Enterprise Agreement](https://www.microsoft.com/en-us/licensing/licensing-programs/enterprise.aspx), the [Open Volume License Program](https://www.microsoft.com/en-us/licensing/licensing-programs/open-license.aspx), and the [Cloud Solution Providers program](https://partner.microsoft.com/cloud-solution-provider).</span><span class="sxs-lookup"><span data-stu-id="e7fdb-118">Azure AD Premium P2 is available through a [Microsoft Enterprise Agreement](https://www.microsoft.com/en-us/licensing/licensing-programs/enterprise.aspx), the [Open Volume License Program](https://www.microsoft.com/en-us/licensing/licensing-programs/open-license.aspx), and the [Cloud Solution Providers program](https://partner.microsoft.com/cloud-solution-provider).</span></span> <span data-ttu-id="e7fdb-119">Azure and Office 365 subscribers can also buy Azure AD Premium P2 online.</span><span class="sxs-lookup"><span data-stu-id="e7fdb-119">Azure and Office 365 subscribers can also buy Azure AD Premium P2 online.</span></span>  <span data-ttu-id="e7fdb-120">More information on Azure AD Premium pricing and how to order online can be found at [Azure Active Directory Pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="e7fdb-120">More information on Azure AD Premium pricing and how to order online can be found at [Azure Active Directory Pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

## <a name="azure-ad-privileged-identity-management-is-not-available-in-tenant"></a><span data-ttu-id="e7fdb-121">Azure AD Privileged Identity Management is not available in tenant</span><span class="sxs-lookup"><span data-stu-id="e7fdb-121">Azure AD Privileged Identity Management is not available in tenant</span></span>

<span data-ttu-id="e7fdb-122">Azure AD Privileged Identity Management will no longer be available in your tenant if:</span><span class="sxs-lookup"><span data-stu-id="e7fdb-122">Azure AD Privileged Identity Management will no longer be available in your tenant if:</span></span>
- <span data-ttu-id="e7fdb-123">Your organization was using Azure AD Privileged Identity Management when it was in preview and does not purchase Azure AD Premium P2 subscription or EMS E5 subscription.</span><span class="sxs-lookup"><span data-stu-id="e7fdb-123">Your organization was using Azure AD Privileged Identity Management when it was in preview and does not purchase Azure AD Premium P2 subscription or EMS E5 subscription.</span></span>
- <span data-ttu-id="e7fdb-124">Your organization had an Azure AD Premium P2 or EMS E5 trial that expired.</span><span class="sxs-lookup"><span data-stu-id="e7fdb-124">Your organization had an Azure AD Premium P2 or EMS E5 trial that expired.</span></span>
- <span data-ttu-id="e7fdb-125">Your organization had a purchased subscription that expired.</span><span class="sxs-lookup"><span data-stu-id="e7fdb-125">Your organization had a purchased subscription that expired.</span></span>

<span data-ttu-id="e7fdb-126">When an Azure AD Premium P2 subscription or EMS E5 subscription expires, or an organization that was using Azure AD Privileged Identity Management in preview does not obtain Azure AD Premium P2 or EMS E5 subscription:</span><span class="sxs-lookup"><span data-stu-id="e7fdb-126">When an Azure AD Premium P2 subscription or EMS E5 subscription expires, or an organization that was using Azure AD Privileged Identity Management in preview does not obtain Azure AD Premium P2 or EMS E5 subscription:</span></span>

- <span data-ttu-id="e7fdb-127">Permanent role assignments to Azure AD roles will be unaffected.</span><span class="sxs-lookup"><span data-stu-id="e7fdb-127">Permanent role assignments to Azure AD roles will be unaffected.</span></span>
- <span data-ttu-id="e7fdb-128">The Azure AD Privileged Identity Management extension in the Azure portal, as well as the Graph API cmdlets and PowerShell interfaces of Azure AD Privileged Identity Management, will no longer be available for users to activate privileged roles, manage privileged access, or perform access reviews of privileged roles.</span><span class="sxs-lookup"><span data-stu-id="e7fdb-128">The Azure AD Privileged Identity Management extension in the Azure portal, as well as the Graph API cmdlets and PowerShell interfaces of Azure AD Privileged Identity Management, will no longer be available for users to activate privileged roles, manage privileged access, or perform access reviews of privileged roles.</span></span>
- <span data-ttu-id="e7fdb-129">Eligible role assignments of Azure AD roles will be removed, as users will no longer be able to activate privileged roles.</span><span class="sxs-lookup"><span data-stu-id="e7fdb-129">Eligible role assignments of Azure AD roles will be removed, as users will no longer be able to activate privileged roles.</span></span>
- <span data-ttu-id="e7fdb-130">Any ongoing access reviews of Azure AD roles will end, and Azure AD Privileged Identity Management configuration settings will be removed.</span><span class="sxs-lookup"><span data-stu-id="e7fdb-130">Any ongoing access reviews of Azure AD roles will end, and Azure AD Privileged Identity Management configuration settings will be removed.</span></span>
- <span data-ttu-id="e7fdb-131">Azure AD Privileged Identity Management will no longer send emails on role assignment changes.</span><span class="sxs-lookup"><span data-stu-id="e7fdb-131">Azure AD Privileged Identity Management will no longer send emails on role assignment changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e7fdb-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="e7fdb-132">Next steps</span></span>

- [<span data-ttu-id="e7fdb-133">Start using PIM</span><span class="sxs-lookup"><span data-stu-id="e7fdb-133">Start using PIM</span></span>](pim-getting-started.md)
- [<span data-ttu-id="e7fdb-134">Azure AD directory roles you can manage in PIM</span><span class="sxs-lookup"><span data-stu-id="e7fdb-134">Azure AD directory roles you can manage in PIM</span></span>](pim-roles.md)
