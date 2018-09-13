---
title: Secure cloud resources with Azure MFA and AD FS | Microsoft Docs
description: This is the Azure Multi-Factor authentication page that describes how to get started with Azure MFA and AD FS in the cloud.
services: multi-factor-authentication
documentationcenter: ''
author: kgremban
manager: femila
editor: yossib
ms.assetid: 0927fc67-8090-4fdd-913a-b3cfed3fbe77
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/09/2017
ms.author: kgremban
ms.openlocfilehash: a93a9edc85164b33d1ff4f44d446a64a357be705
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550489"
---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a><span data-ttu-id="bba7d-103">Securing cloud resources with Azure Multi-Factor Authentication and AD FS</span><span class="sxs-lookup"><span data-stu-id="bba7d-103">Securing cloud resources with Azure Multi-Factor Authentication and AD FS</span></span>
<span data-ttu-id="bba7d-104">If your organization is federated with Azure Active Directory, use Azure Multi-Factor Authentication or Active Directory Federation Services (AD FS) to secure resources that are accessed by Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bba7d-104">If your organization is federated with Azure Active Directory, use Azure Multi-Factor Authentication or Active Directory Federation Services (AD FS) to secure resources that are accessed by Azure AD.</span></span> <span data-ttu-id="bba7d-105">Use the following procedures to secure Azure Active Directory resources with either Azure Multi-Factor Authentication or Active Directory Federation Services.</span><span class="sxs-lookup"><span data-stu-id="bba7d-105">Use the following procedures to secure Azure Active Directory resources with either Azure Multi-Factor Authentication or Active Directory Federation Services.</span></span>

## <a name="secure-azure-ad-resources-using-ad-fs"></a><span data-ttu-id="bba7d-106">Secure Azure AD resources using AD FS</span><span class="sxs-lookup"><span data-stu-id="bba7d-106">Secure Azure AD resources using AD FS</span></span>
<span data-ttu-id="bba7d-107">To secure your cloud resource, set up a claims rule so that Active Directory Federation Services emits the multipleauthn claim when a user performs two-step verification successfully.</span><span class="sxs-lookup"><span data-stu-id="bba7d-107">To secure your cloud resource, set up a claims rule so that Active Directory Federation Services emits the multipleauthn claim when a user performs two-step verification successfully.</span></span> <span data-ttu-id="bba7d-108">This claim is passed on to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bba7d-108">This claim is passed on to Azure AD.</span></span> <span data-ttu-id="bba7d-109">Follow this procedure to walk through the steps:</span><span class="sxs-lookup"><span data-stu-id="bba7d-109">Follow this procedure to walk through the steps:</span></span>


1. <span data-ttu-id="bba7d-110">Open AD FS Management.</span><span class="sxs-lookup"><span data-stu-id="bba7d-110">Open AD FS Management.</span></span>
2. <span data-ttu-id="bba7d-111">On the left, select **Relying Party Trusts**.</span><span class="sxs-lookup"><span data-stu-id="bba7d-111">On the left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="bba7d-112">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules…**</span><span class="sxs-lookup"><span data-stu-id="bba7d-112">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules…**</span></span>

   ![Cloud](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. <span data-ttu-id="bba7d-114">On Issuance Transform Rules, click **Add Rule.**</span><span class="sxs-lookup"><span data-stu-id="bba7d-114">On Issuance Transform Rules, click **Add Rule.**</span></span>

   ![Cloud](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. <span data-ttu-id="bba7d-116">On the Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from the drop-down and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bba7d-116">On the Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from the drop-down and click **Next**.</span></span>

   ![Cloud](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. <span data-ttu-id="bba7d-118">Give your rule a name.</span><span class="sxs-lookup"><span data-stu-id="bba7d-118">Give your rule a name.</span></span> 
7. <span data-ttu-id="bba7d-119">Select **Authentication Methods References** as the Incoming claim type.</span><span class="sxs-lookup"><span data-stu-id="bba7d-119">Select **Authentication Methods References** as the Incoming claim type.</span></span>
8. <span data-ttu-id="bba7d-120">Select **Pass through all claim values**.</span><span class="sxs-lookup"><span data-stu-id="bba7d-120">Select **Pass through all claim values**.</span></span>
    <span data-ttu-id="bba7d-121">![Add Transform Claim Rule Wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span><span class="sxs-lookup"><span data-stu-id="bba7d-121">![Add Transform Claim Rule Wizard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span></span>
9. <span data-ttu-id="bba7d-122">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="bba7d-122">Click **Finish**.</span></span> <span data-ttu-id="bba7d-123">Close the AD FS Management console.</span><span class="sxs-lookup"><span data-stu-id="bba7d-123">Close the AD FS Management console.</span></span>

## <a name="trusted-ips-for-federated-users"></a><span data-ttu-id="bba7d-124">Trusted IPs for federated users</span><span class="sxs-lookup"><span data-stu-id="bba7d-124">Trusted IPs for federated users</span></span>
<span data-ttu-id="bba7d-125">Trusted IPs allow administrators to by-pass two-step verification for specific IP addresses, or for federated users that have requests originating from within their own intranet.</span><span class="sxs-lookup"><span data-stu-id="bba7d-125">Trusted IPs allow administrators to by-pass two-step verification for specific IP addresses, or for federated users that have requests originating from within their own intranet.</span></span> <span data-ttu-id="bba7d-126">The following sections describe how to configure Azure Multi-Factor Authentication Trusted IPs with federated users and by-pass two-step verification when a request originates from within a federated users intranet.</span><span class="sxs-lookup"><span data-stu-id="bba7d-126">The following sections describe how to configure Azure Multi-Factor Authentication Trusted IPs with federated users and by-pass two-step verification when a request originates from within a federated users intranet.</span></span> <span data-ttu-id="bba7d-127">This is achieved by configuring AD FS to use a pass-through or filter an incoming claim template with the Inside Corporate Network claim type.</span><span class="sxs-lookup"><span data-stu-id="bba7d-127">This is achieved by configuring AD FS to use a pass-through or filter an incoming claim template with the Inside Corporate Network claim type.</span></span>

<span data-ttu-id="bba7d-128">This example uses Office 365 for our Relying Party Trusts.</span><span class="sxs-lookup"><span data-stu-id="bba7d-128">This example uses Office 365 for our Relying Party Trusts.</span></span>

### <a name="configure-the-ad-fs-claims-rules"></a><span data-ttu-id="bba7d-129">Configure the AD FS claims rules</span><span class="sxs-lookup"><span data-stu-id="bba7d-129">Configure the AD FS claims rules</span></span>
<span data-ttu-id="bba7d-130">The first thing we need to do is to configure the AD FS claims.</span><span class="sxs-lookup"><span data-stu-id="bba7d-130">The first thing we need to do is to configure the AD FS claims.</span></span> <span data-ttu-id="bba7d-131">Create two claims rules, one for the Inside Corporate Network claim type and an additional one for keeping our users signed in.</span><span class="sxs-lookup"><span data-stu-id="bba7d-131">Create two claims rules, one for the Inside Corporate Network claim type and an additional one for keeping our users signed in.</span></span>

1. <span data-ttu-id="bba7d-132">Open AD FS Management.</span><span class="sxs-lookup"><span data-stu-id="bba7d-132">Open AD FS Management.</span></span>
2. <span data-ttu-id="bba7d-133">On the left, select **Relying Party Trusts**.</span><span class="sxs-lookup"><span data-stu-id="bba7d-133">On the left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="bba7d-134">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules…**
   ![Cloud](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span><span class="sxs-lookup"><span data-stu-id="bba7d-134">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules…**
![Cloud](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span></span>
4. <span data-ttu-id="bba7d-135">On Issuance Transform Rules, click **Add Rule.**
   ![Cloud](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span><span class="sxs-lookup"><span data-stu-id="bba7d-135">On Issuance Transform Rules, click **Add Rule.**
![Cloud](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span></span>
5. <span data-ttu-id="bba7d-136">On the Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from the drop-down and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bba7d-136">On the Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from the drop-down and click **Next**.</span></span>
   <span data-ttu-id="bba7d-137">![Cloud](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span><span class="sxs-lookup"><span data-stu-id="bba7d-137">![Cloud](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span></span>
6. <span data-ttu-id="bba7d-138">In the box next to Claim rule name, give your rule a name.</span><span class="sxs-lookup"><span data-stu-id="bba7d-138">In the box next to Claim rule name, give your rule a name.</span></span> <span data-ttu-id="bba7d-139">For example: InsideCorpNet.</span><span class="sxs-lookup"><span data-stu-id="bba7d-139">For example: InsideCorpNet.</span></span>
7. <span data-ttu-id="bba7d-140">From the drop-down, next to Incoming claim type, select **Inside Corporate Network**.</span><span class="sxs-lookup"><span data-stu-id="bba7d-140">From the drop-down, next to Incoming claim type, select **Inside Corporate Network**.</span></span>
   <span data-ttu-id="bba7d-141">![Cloud](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span><span class="sxs-lookup"><span data-stu-id="bba7d-141">![Cloud](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span></span>
8. <span data-ttu-id="bba7d-142">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="bba7d-142">Click **Finish**.</span></span>
9. <span data-ttu-id="bba7d-143">On Issuance Transform Rules, click **Add Rule**.</span><span class="sxs-lookup"><span data-stu-id="bba7d-143">On Issuance Transform Rules, click **Add Rule**.</span></span>
10. <span data-ttu-id="bba7d-144">On the Add Transform Claim Rule Wizard, select **Send Claims Using a Custom Rule** from the drop-down and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bba7d-144">On the Add Transform Claim Rule Wizard, select **Send Claims Using a Custom Rule** from the drop-down and click **Next**.</span></span>
11. <span data-ttu-id="bba7d-145">In the box under Claim rule name: enter *Keep Users Signed In*.</span><span class="sxs-lookup"><span data-stu-id="bba7d-145">In the box under Claim rule name: enter *Keep Users Signed In*.</span></span>
12. <span data-ttu-id="bba7d-146">In the Custom rule box, enter:</span><span class="sxs-lookup"><span data-stu-id="bba7d-146">In the Custom rule box, enter:</span></span>

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![Cloud](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-adfs-cloud/trustedip5.png)
13. <span data-ttu-id="bba7d-148">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="bba7d-148">Click **Finish**.</span></span>
14. <span data-ttu-id="bba7d-149">Click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="bba7d-149">Click **Apply**.</span></span>
15. <span data-ttu-id="bba7d-150">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="bba7d-150">Click **Ok**.</span></span>
16. <span data-ttu-id="bba7d-151">Close AD FS Management.</span><span class="sxs-lookup"><span data-stu-id="bba7d-151">Close AD FS Management.</span></span>

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a><span data-ttu-id="bba7d-152">Configure Azure Multi-Factor Authentication Trusted IPs with Federated Users</span><span class="sxs-lookup"><span data-stu-id="bba7d-152">Configure Azure Multi-Factor Authentication Trusted IPs with Federated Users</span></span>
<span data-ttu-id="bba7d-153">Now that the claims are in place, we can configure trusted IPs.</span><span class="sxs-lookup"><span data-stu-id="bba7d-153">Now that the claims are in place, we can configure trusted IPs.</span></span>

1. <span data-ttu-id="bba7d-154">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="bba7d-154">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="bba7d-155">On the left, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bba7d-155">On the left, click **Active Directory**.</span></span>
3. <span data-ttu-id="bba7d-156">Under Directory, select the directory where you want to set up trusted IPs.</span><span class="sxs-lookup"><span data-stu-id="bba7d-156">Under Directory, select the directory where you want to set up trusted IPs.</span></span>
4. <span data-ttu-id="bba7d-157">On the Directory you have selected, click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="bba7d-157">On the Directory you have selected, click **Configure**.</span></span>
5. <span data-ttu-id="bba7d-158">In the multi-factor authentication section, click **Manage service settings**.</span><span class="sxs-lookup"><span data-stu-id="bba7d-158">In the multi-factor authentication section, click **Manage service settings**.</span></span>
6. <span data-ttu-id="bba7d-159">On the Service Settings page, under trusted IPs, select **Skip multi-factor-authentication for requests from federated users on my intranet.**
   ![Cloud](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)</span><span class="sxs-lookup"><span data-stu-id="bba7d-159">On the Service Settings page, under trusted IPs, select **Skip multi-factor-authentication for requests from federated users on my intranet.**
![Cloud](https://docstestmedia1.blob.core.windows.net/azure-media/articles/multi-factor-authentication/media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)</span></span>
7. <span data-ttu-id="bba7d-160">Click **save**.</span><span class="sxs-lookup"><span data-stu-id="bba7d-160">Click **save**.</span></span>
8. <span data-ttu-id="bba7d-161">Once the updates have been applied, click **close**.</span><span class="sxs-lookup"><span data-stu-id="bba7d-161">Once the updates have been applied, click **close**.</span></span>

<span data-ttu-id="bba7d-162">That’s it!</span><span class="sxs-lookup"><span data-stu-id="bba7d-162">That’s it!</span></span> <span data-ttu-id="bba7d-163">At this point, federated Office 365 users should only have to use MFA when a claim originates from outside the corporate intranet.</span><span class="sxs-lookup"><span data-stu-id="bba7d-163">At this point, federated Office 365 users should only have to use MFA when a claim originates from outside the corporate intranet.</span></span>










