---
title: Set up SharePoint Online and Exchange Online for Azure Active Directory conditional access | Microsoft Docs
description: Learn how to set up SharePoint Online and Exchange Online for Azure Active Directory conditional access.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: mtillman
editor: ''
ms.assetid: 62349fba-3cc0-4ab5-babe-372b3389eff6
ms.service: active-directory
ms.component: protection
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/15/2018
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: ed1937dd29abebc4b81dde41618c56ecb5ebdccc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869992"
---
# <a name="how-to-set-up-sharepoint-online-and-exchange-online-for-azure-active-directory-conditional-access"></a><span data-ttu-id="95c38-103">How To: Set up SharePoint Online and Exchange Online for Azure Active Directory conditional access</span><span class="sxs-lookup"><span data-stu-id="95c38-103">How To: Set up SharePoint Online and Exchange Online for Azure Active Directory conditional access</span></span> 

<span data-ttu-id="95c38-104">With [Azure Active Directory (Azure AD) conditional access](overview.md), you can control how users access your cloud apps.</span><span class="sxs-lookup"><span data-stu-id="95c38-104">With [Azure Active Directory (Azure AD) conditional access](overview.md), you can control how users access your cloud apps.</span></span> <span data-ttu-id="95c38-105">If you want to use conditional access to control access to SharePoint and Exchange online, you need to:</span><span class="sxs-lookup"><span data-stu-id="95c38-105">If you want to use conditional access to control access to SharePoint and Exchange online, you need to:</span></span>

- <span data-ttu-id="95c38-106">Review whether your conditional access scenario is supported</span><span class="sxs-lookup"><span data-stu-id="95c38-106">Review whether your conditional access scenario is supported</span></span>
- <span data-ttu-id="95c38-107">Prevent client apps from bypassing the enforcement of your conditional access policies.</span><span class="sxs-lookup"><span data-stu-id="95c38-107">Prevent client apps from bypassing the enforcement of your conditional access policies.</span></span>   

<span data-ttu-id="95c38-108">This article explains, how you can address both cases.</span><span class="sxs-lookup"><span data-stu-id="95c38-108">This article explains, how you can address both cases.</span></span>


## <a name="what-you-need-to-know"></a><span data-ttu-id="95c38-109">What you need to know</span><span class="sxs-lookup"><span data-stu-id="95c38-109">What you need to know</span></span>

<span data-ttu-id="95c38-110">You can use Azure AD conditional access to protect cloud apps when an authentication attempt comes from:</span><span class="sxs-lookup"><span data-stu-id="95c38-110">You can use Azure AD conditional access to protect cloud apps when an authentication attempt comes from:</span></span>

- <span data-ttu-id="95c38-111">A web browser</span><span class="sxs-lookup"><span data-stu-id="95c38-111">A web browser</span></span>

- <span data-ttu-id="95c38-112">A client app that uses [modern authentication](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a)</span><span class="sxs-lookup"><span data-stu-id="95c38-112">A client app that uses [modern authentication](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a)</span></span>

- <span data-ttu-id="95c38-113">Exchange ActiveSync</span><span class="sxs-lookup"><span data-stu-id="95c38-113">Exchange ActiveSync</span></span> 

<span data-ttu-id="95c38-114">Some cloud apps also support legacy authentication protocols.</span><span class="sxs-lookup"><span data-stu-id="95c38-114">Some cloud apps also support legacy authentication protocols.</span></span> <span data-ttu-id="95c38-115">This applies, for example, to SharePoint Online and Exchange Online.</span><span class="sxs-lookup"><span data-stu-id="95c38-115">This applies, for example, to SharePoint Online and Exchange Online.</span></span> <span data-ttu-id="95c38-116">When a client app can use a legacy authentication protocol to access a cloud app, Azure AD cannot enforce a conditional access policy on this access attempt.</span><span class="sxs-lookup"><span data-stu-id="95c38-116">When a client app can use a legacy authentication protocol to access a cloud app, Azure AD cannot enforce a conditional access policy on this access attempt.</span></span> <span data-ttu-id="95c38-117">To prevent a client app from bypassing the enforcement of policies, you should check whether it is possible to only enable modern authentication on the affected cloud apps.</span><span class="sxs-lookup"><span data-stu-id="95c38-117">To prevent a client app from bypassing the enforcement of policies, you should check whether it is possible to only enable modern authentication on the affected cloud apps.</span></span> 

<span data-ttu-id="95c38-118">Examples for client apps conditional access does not apply to are:</span><span class="sxs-lookup"><span data-stu-id="95c38-118">Examples for client apps conditional access does not apply to are:</span></span>

- <span data-ttu-id="95c38-119">Office 2010 and earlier</span><span class="sxs-lookup"><span data-stu-id="95c38-119">Office 2010 and earlier</span></span>

- <span data-ttu-id="95c38-120">Office 2013 when modern authentication is not enabled</span><span class="sxs-lookup"><span data-stu-id="95c38-120">Office 2013 when modern authentication is not enabled</span></span>



 
## <a name="control-access-to-sharepoint-online"></a><span data-ttu-id="95c38-121">Control access to SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="95c38-121">Control access to SharePoint Online</span></span>

<span data-ttu-id="95c38-122">In addition to modern authentication, SharePoint Online also supports legacy authentication protocols.</span><span class="sxs-lookup"><span data-stu-id="95c38-122">In addition to modern authentication, SharePoint Online also supports legacy authentication protocols.</span></span> <span data-ttu-id="95c38-123">If the legacy authentication protocols are enabled, your conditional access policies for SharePoint are not enforced for clients that don't use modern authentication.</span><span class="sxs-lookup"><span data-stu-id="95c38-123">If the legacy authentication protocols are enabled, your conditional access policies for SharePoint are not enforced for clients that don't use modern authentication.</span></span>

<span data-ttu-id="95c38-124">You can disable legacy authentication protocols for SharePoint access by using the **[Set-SPOTenant](https://technet.microsoft.com/library/fp161390.aspx)** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="95c38-124">You can disable legacy authentication protocols for SharePoint access by using the **[Set-SPOTenant](https://technet.microsoft.com/library/fp161390.aspx)** cmdlet:</span></span> 

    Set-SPOTenant -LegacyAuthProtocolsEnabled $false

## <a name="control-access-to-exchange-online"></a><span data-ttu-id="95c38-125">Control access to Exchange Online</span><span class="sxs-lookup"><span data-stu-id="95c38-125">Control access to Exchange Online</span></span>

<span data-ttu-id="95c38-126">When you set up conditional access policies for Exchange Online, you need to review the following:</span><span class="sxs-lookup"><span data-stu-id="95c38-126">When you set up conditional access policies for Exchange Online, you need to review the following:</span></span>

- <span data-ttu-id="95c38-127">Exchange ActiveSync</span><span class="sxs-lookup"><span data-stu-id="95c38-127">Exchange ActiveSync</span></span>

- <span data-ttu-id="95c38-128">Legacy authentication protocols</span><span class="sxs-lookup"><span data-stu-id="95c38-128">Legacy authentication protocols</span></span>



### <a name="exchange-activesync"></a><span data-ttu-id="95c38-129">Exchange ActiveSync</span><span class="sxs-lookup"><span data-stu-id="95c38-129">Exchange ActiveSync</span></span>

<span data-ttu-id="95c38-130">While Exchange Active Sync supports modern authentication, there are some limitations regarding the support for conditional access scenarios:</span><span class="sxs-lookup"><span data-stu-id="95c38-130">While Exchange Active Sync supports modern authentication, there are some limitations regarding the support for conditional access scenarios:</span></span>

- <span data-ttu-id="95c38-131">You can only configure the device platforms condition</span><span class="sxs-lookup"><span data-stu-id="95c38-131">You can only configure the device platforms condition</span></span>  

    ![Device platforms](./media/conditional-access-for-exo-and-spo/05.png)

- <span data-ttu-id="95c38-133">Setting the multi-factor authentication requirement is not supported</span><span class="sxs-lookup"><span data-stu-id="95c38-133">Setting the multi-factor authentication requirement is not supported</span></span>  

    ![Conditional access](./media/conditional-access-for-exo-and-spo/01.png)

<span data-ttu-id="95c38-135">To effectively protect access to Exchange Online from Exchange ActiveSync, you can:</span><span class="sxs-lookup"><span data-stu-id="95c38-135">To effectively protect access to Exchange Online from Exchange ActiveSync, you can:</span></span>

- <span data-ttu-id="95c38-136">Configure a supported conditional access policy by following these steps:</span><span class="sxs-lookup"><span data-stu-id="95c38-136">Configure a supported conditional access policy by following these steps:</span></span>

    <span data-ttu-id="95c38-137">a.</span><span class="sxs-lookup"><span data-stu-id="95c38-137">a.</span></span> <span data-ttu-id="95c38-138">Select just **Office 365 Exchange Online** as cloud app.</span><span class="sxs-lookup"><span data-stu-id="95c38-138">Select just **Office 365 Exchange Online** as cloud app.</span></span>  

    ![Conditional access](./media/conditional-access-for-exo-and-spo/04.png)

    <span data-ttu-id="95c38-140">b.</span><span class="sxs-lookup"><span data-stu-id="95c38-140">b.</span></span> <span data-ttu-id="95c38-141">Select **Exchange Active Sync** as **client app**, and then select **Apply policy only to supported platforms**.</span><span class="sxs-lookup"><span data-stu-id="95c38-141">Select **Exchange Active Sync** as **client app**, and then select **Apply policy only to supported platforms**.</span></span>  

    ![Device platforms](./media/conditional-access-for-exo-and-spo/03.png)

- <span data-ttu-id="95c38-143">Block Exchange ActiveSync by using Active Directory Federation Services (AD FS) rules.</span><span class="sxs-lookup"><span data-stu-id="95c38-143">Block Exchange ActiveSync by using Active Directory Federation Services (AD FS) rules.</span></span>

        @RuleName = "Block Exchange ActiveSync"
        c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value == "Microsoft.Exchange.ActiveSync"]
        => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "false");




### <a name="legacy-authentication-protocols"></a><span data-ttu-id="95c38-144">Legacy authentication protocols</span><span class="sxs-lookup"><span data-stu-id="95c38-144">Legacy authentication protocols</span></span>

<span data-ttu-id="95c38-145">In addition to modern authentication, Exchange Online also supports legacy authentication protocols.</span><span class="sxs-lookup"><span data-stu-id="95c38-145">In addition to modern authentication, Exchange Online also supports legacy authentication protocols.</span></span> <span data-ttu-id="95c38-146">If legacy authentication protocols are enabled, your conditional access policies for Exchange Online are not enforced for clients that don't use modern authentication.</span><span class="sxs-lookup"><span data-stu-id="95c38-146">If legacy authentication protocols are enabled, your conditional access policies for Exchange Online are not enforced for clients that don't use modern authentication.</span></span>

<span data-ttu-id="95c38-147">You can disable legacy authentication protocols for Exchange Online by setting AD FS rules.</span><span class="sxs-lookup"><span data-stu-id="95c38-147">You can disable legacy authentication protocols for Exchange Online by setting AD FS rules.</span></span> <span data-ttu-id="95c38-148">This blocks access from:</span><span class="sxs-lookup"><span data-stu-id="95c38-148">This blocks access from:</span></span>

- <span data-ttu-id="95c38-149">Older Office clients, such as Office 2013 that don't have modern authentication enabled</span><span class="sxs-lookup"><span data-stu-id="95c38-149">Older Office clients, such as Office 2013 that don't have modern authentication enabled</span></span> 

- <span data-ttu-id="95c38-150">Earlier versions of Office</span><span class="sxs-lookup"><span data-stu-id="95c38-150">Earlier versions of Office</span></span>


## <a name="set-up-ad-fs-rules"></a><span data-ttu-id="95c38-151">Set up AD FS rules</span><span class="sxs-lookup"><span data-stu-id="95c38-151">Set up AD FS rules</span></span>

<span data-ttu-id="95c38-152">You can use the following issuance authorization rules to enable or block traffic at the AD FS level.</span><span class="sxs-lookup"><span data-stu-id="95c38-152">You can use the following issuance authorization rules to enable or block traffic at the AD FS level.</span></span> 

### <a name="block-legacy-traffic-from-the-extranet"></a><span data-ttu-id="95c38-153">Block legacy traffic from the extranet</span><span class="sxs-lookup"><span data-stu-id="95c38-153">Block legacy traffic from the extranet</span></span>

<span data-ttu-id="95c38-154">By applying the following three rules:</span><span class="sxs-lookup"><span data-stu-id="95c38-154">By applying the following three rules:</span></span> 

- <span data-ttu-id="95c38-155">You enable access for:</span><span class="sxs-lookup"><span data-stu-id="95c38-155">You enable access for:</span></span>
    - <span data-ttu-id="95c38-156">Exchange ActiveSync traffic</span><span class="sxs-lookup"><span data-stu-id="95c38-156">Exchange ActiveSync traffic</span></span>
    - <span data-ttu-id="95c38-157">Browser traffic</span><span class="sxs-lookup"><span data-stu-id="95c38-157">Browser traffic</span></span>
    - <span data-ttu-id="95c38-158">Modern authentication traffic</span><span class="sxs-lookup"><span data-stu-id="95c38-158">Modern authentication traffic</span></span>
- <span data-ttu-id="95c38-159">You block access for:</span><span class="sxs-lookup"><span data-stu-id="95c38-159">You block access for:</span></span> 
    - <span data-ttu-id="95c38-160">Legacy client apps from the extranet</span><span class="sxs-lookup"><span data-stu-id="95c38-160">Legacy client apps from the extranet</span></span>

<span data-ttu-id="95c38-161">**Rule 1:**</span><span class="sxs-lookup"><span data-stu-id="95c38-161">**Rule 1:**</span></span>

    @RuleName = "Allow all intranet traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "true"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

<span data-ttu-id="95c38-162">**Rule 2:**</span><span class="sxs-lookup"><span data-stu-id="95c38-162">**Rule 2:**</span></span>

    @RuleName = "Allow Exchange ActiveSync"
    c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value == "Microsoft.Exchange.ActiveSync"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

<span data-ttu-id="95c38-163">**Rule 3:**</span><span class="sxs-lookup"><span data-stu-id="95c38-163">**Rule 3:**</span></span>

    @RuleName = "Allow extranet browser and browser dialog traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

### <a name="block-legacy-traffic-from-anywhere"></a><span data-ttu-id="95c38-164">Block legacy traffic from anywhere</span><span class="sxs-lookup"><span data-stu-id="95c38-164">Block legacy traffic from anywhere</span></span>

<span data-ttu-id="95c38-165">By applying the following three rules:</span><span class="sxs-lookup"><span data-stu-id="95c38-165">By applying the following three rules:</span></span>

- <span data-ttu-id="95c38-166">You enable access for:</span><span class="sxs-lookup"><span data-stu-id="95c38-166">You enable access for:</span></span> 
    - <span data-ttu-id="95c38-167">Exchange ActiveSync traffic</span><span class="sxs-lookup"><span data-stu-id="95c38-167">Exchange ActiveSync traffic</span></span>
    - <span data-ttu-id="95c38-168">Browser traffic</span><span class="sxs-lookup"><span data-stu-id="95c38-168">Browser traffic</span></span>
    - <span data-ttu-id="95c38-169">Modern authentication traffic</span><span class="sxs-lookup"><span data-stu-id="95c38-169">Modern authentication traffic</span></span>
- <span data-ttu-id="95c38-170">You block access for:</span><span class="sxs-lookup"><span data-stu-id="95c38-170">You block access for:</span></span> 
    - <span data-ttu-id="95c38-171">Legacy apps from any location</span><span class="sxs-lookup"><span data-stu-id="95c38-171">Legacy apps from any location</span></span>

##### <a name="rule-1"></a><span data-ttu-id="95c38-172">Rule 1</span><span class="sxs-lookup"><span data-stu-id="95c38-172">Rule 1</span></span>
    @RuleName = "Allow all intranet traffic only for browser and modern authentication clients"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "true"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


##### <a name="rule-2"></a><span data-ttu-id="95c38-173">Rule 2</span><span class="sxs-lookup"><span data-stu-id="95c38-173">Rule 2</span></span>
    @RuleName = "Allow Exchange ActiveSync"
    c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value == "Microsoft.Exchange.ActiveSync"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


##### <a name="rule-3"></a><span data-ttu-id="95c38-174">Rule 3</span><span class="sxs-lookup"><span data-stu-id="95c38-174">Rule 3</span></span>
    @RuleName = "Allow extranet browser and browser dialog traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

## <a name="next-steps"></a><span data-ttu-id="95c38-175">Next steps</span><span class="sxs-lookup"><span data-stu-id="95c38-175">Next steps</span></span>

<span data-ttu-id="95c38-176">For more information, see [What is conditional access in Azure Active Directory](overview.md).</span><span class="sxs-lookup"><span data-stu-id="95c38-176">For more information, see [What is conditional access in Azure Active Directory](overview.md).</span></span>

<span data-ttu-id="95c38-177">For instructions about configuring claim rules, see [Configure Claim Rules](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configure-claim-rules).</span><span class="sxs-lookup"><span data-stu-id="95c38-177">For instructions about configuring claim rules, see [Configure Claim Rules](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configure-claim-rules).</span></span> 






