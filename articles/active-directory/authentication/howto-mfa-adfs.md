---
title: Secure cloud resources with Azure MFA and AD FS | Microsoft Docs
description: This is the Azure Multi-Factor authentication page that describes how to get started with Azure MFA and AD FS in the cloud.
services: multi-factor-authentication
ms.service: active-directory
ms.component: authentication
ms.topic: conceptual
ms.date: 07/11/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: michmcla
ms.openlocfilehash: afb28488fc47f018b6d192eb1b65a54499ac8ff9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965600"
---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a><span data-ttu-id="e393e-103">Securing cloud resources with Azure Multi-Factor Authentication and AD FS</span><span class="sxs-lookup"><span data-stu-id="e393e-103">Securing cloud resources with Azure Multi-Factor Authentication and AD FS</span></span>

<span data-ttu-id="e393e-104">If your organization is federated with Azure Active Directory, use Azure Multi-Factor Authentication or Active Directory Federation Services (AD FS) to secure resources that are accessed by Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e393e-104">If your organization is federated with Azure Active Directory, use Azure Multi-Factor Authentication or Active Directory Federation Services (AD FS) to secure resources that are accessed by Azure AD.</span></span> <span data-ttu-id="e393e-105">Use the following procedures to secure Azure Active Directory resources with either Azure Multi-Factor Authentication or Active Directory Federation Services.</span><span class="sxs-lookup"><span data-stu-id="e393e-105">Use the following procedures to secure Azure Active Directory resources with either Azure Multi-Factor Authentication or Active Directory Federation Services.</span></span>

## <a name="secure-azure-ad-resources-using-ad-fs"></a><span data-ttu-id="e393e-106">Secure Azure AD resources using AD FS</span><span class="sxs-lookup"><span data-stu-id="e393e-106">Secure Azure AD resources using AD FS</span></span>

<span data-ttu-id="e393e-107">To secure your cloud resource, set up a claims rule so that Active Directory Federation Services emits the multipleauthn claim when a user performs two-step verification successfully.</span><span class="sxs-lookup"><span data-stu-id="e393e-107">To secure your cloud resource, set up a claims rule so that Active Directory Federation Services emits the multipleauthn claim when a user performs two-step verification successfully.</span></span> <span data-ttu-id="e393e-108">This claim is passed on to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e393e-108">This claim is passed on to Azure AD.</span></span> <span data-ttu-id="e393e-109">Follow this procedure to walk through the steps:</span><span class="sxs-lookup"><span data-stu-id="e393e-109">Follow this procedure to walk through the steps:</span></span>

1. <span data-ttu-id="e393e-110">Open AD FS Management.</span><span class="sxs-lookup"><span data-stu-id="e393e-110">Open AD FS Management.</span></span>
2. <span data-ttu-id="e393e-111">On the left, select **Relying Party Trusts**.</span><span class="sxs-lookup"><span data-stu-id="e393e-111">On the left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="e393e-112">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules**.</span><span class="sxs-lookup"><span data-stu-id="e393e-112">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules**.</span></span>

   ![Cloud](./media/howto-mfa-adfs/trustedip1.png)

4. <span data-ttu-id="e393e-114">On Issuance Transform Rules, click **Add Rule**.</span><span class="sxs-lookup"><span data-stu-id="e393e-114">On Issuance Transform Rules, click **Add Rule**.</span></span>

   ![Cloud](./media/howto-mfa-adfs/trustedip2.png)

5. <span data-ttu-id="e393e-116">On the Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from the drop-down and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e393e-116">On the Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from the drop-down and click **Next**.</span></span>

   ![Cloud](./media/howto-mfa-adfs/trustedip3.png)

6. <span data-ttu-id="e393e-118">Give your rule a name.</span><span class="sxs-lookup"><span data-stu-id="e393e-118">Give your rule a name.</span></span> 
7. <span data-ttu-id="e393e-119">Select **Authentication Methods References** as the Incoming claim type.</span><span class="sxs-lookup"><span data-stu-id="e393e-119">Select **Authentication Methods References** as the Incoming claim type.</span></span>
8. <span data-ttu-id="e393e-120">Select **Pass through all claim values**.</span><span class="sxs-lookup"><span data-stu-id="e393e-120">Select **Pass through all claim values**.</span></span>
    <span data-ttu-id="e393e-121">![Add Transform Claim Rule Wizard](./media/howto-mfa-adfs/configurewizard.png)</span><span class="sxs-lookup"><span data-stu-id="e393e-121">![Add Transform Claim Rule Wizard](./media/howto-mfa-adfs/configurewizard.png)</span></span>
9. <span data-ttu-id="e393e-122">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="e393e-122">Click **Finish**.</span></span> <span data-ttu-id="e393e-123">Close the AD FS Management console.</span><span class="sxs-lookup"><span data-stu-id="e393e-123">Close the AD FS Management console.</span></span>

## <a name="trusted-ips-for-federated-users"></a><span data-ttu-id="e393e-124">Trusted IPs for federated users</span><span class="sxs-lookup"><span data-stu-id="e393e-124">Trusted IPs for federated users</span></span>

<span data-ttu-id="e393e-125">Trusted IPs allow administrators to by-pass two-step verification for specific IP addresses, or for federated users that have requests originating from within their own intranet.</span><span class="sxs-lookup"><span data-stu-id="e393e-125">Trusted IPs allow administrators to by-pass two-step verification for specific IP addresses, or for federated users that have requests originating from within their own intranet.</span></span> <span data-ttu-id="e393e-126">The following sections describe how to configure Azure Multi-Factor Authentication Trusted IPs with federated users and by-pass two-step verification when a request originates from within a federated users intranet.</span><span class="sxs-lookup"><span data-stu-id="e393e-126">The following sections describe how to configure Azure Multi-Factor Authentication Trusted IPs with federated users and by-pass two-step verification when a request originates from within a federated users intranet.</span></span> <span data-ttu-id="e393e-127">This is achieved by configuring AD FS to use a pass-through or filter an incoming claim template with the Inside Corporate Network claim type.</span><span class="sxs-lookup"><span data-stu-id="e393e-127">This is achieved by configuring AD FS to use a pass-through or filter an incoming claim template with the Inside Corporate Network claim type.</span></span>

<span data-ttu-id="e393e-128">This example uses Office 365 for our Relying Party Trusts.</span><span class="sxs-lookup"><span data-stu-id="e393e-128">This example uses Office 365 for our Relying Party Trusts.</span></span>

### <a name="configure-the-ad-fs-claims-rules"></a><span data-ttu-id="e393e-129">Configure the AD FS claims rules</span><span class="sxs-lookup"><span data-stu-id="e393e-129">Configure the AD FS claims rules</span></span>

<span data-ttu-id="e393e-130">The first thing we need to do is to configure the AD FS claims.</span><span class="sxs-lookup"><span data-stu-id="e393e-130">The first thing we need to do is to configure the AD FS claims.</span></span> <span data-ttu-id="e393e-131">Create two claims rules, one for the Inside Corporate Network claim type and an additional one for keeping our users signed in.</span><span class="sxs-lookup"><span data-stu-id="e393e-131">Create two claims rules, one for the Inside Corporate Network claim type and an additional one for keeping our users signed in.</span></span>

1. <span data-ttu-id="e393e-132">Open AD FS Management.</span><span class="sxs-lookup"><span data-stu-id="e393e-132">Open AD FS Management.</span></span>
2. <span data-ttu-id="e393e-133">On the left, select **Relying Party Trusts**.</span><span class="sxs-lookup"><span data-stu-id="e393e-133">On the left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="e393e-134">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules…**
   ![Cloud](./media/howto-mfa-adfs/trustedip1.png)</span><span class="sxs-lookup"><span data-stu-id="e393e-134">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules…**
![Cloud](./media/howto-mfa-adfs/trustedip1.png)</span></span>
4. <span data-ttu-id="e393e-135">On Issuance Transform Rules, click **Add Rule.**
   ![Cloud](./media/howto-mfa-adfs/trustedip2.png)</span><span class="sxs-lookup"><span data-stu-id="e393e-135">On Issuance Transform Rules, click **Add Rule.**
![Cloud](./media/howto-mfa-adfs/trustedip2.png)</span></span>
5. <span data-ttu-id="e393e-136">On the Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from the drop-down and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e393e-136">On the Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from the drop-down and click **Next**.</span></span>
   <span data-ttu-id="e393e-137">![Cloud](./media/howto-mfa-adfs/trustedip3.png)</span><span class="sxs-lookup"><span data-stu-id="e393e-137">![Cloud](./media/howto-mfa-adfs/trustedip3.png)</span></span>
6. <span data-ttu-id="e393e-138">In the box next to Claim rule name, give your rule a name.</span><span class="sxs-lookup"><span data-stu-id="e393e-138">In the box next to Claim rule name, give your rule a name.</span></span> <span data-ttu-id="e393e-139">For example: InsideCorpNet.</span><span class="sxs-lookup"><span data-stu-id="e393e-139">For example: InsideCorpNet.</span></span>
7. <span data-ttu-id="e393e-140">From the drop-down, next to Incoming claim type, select **Inside Corporate Network**.</span><span class="sxs-lookup"><span data-stu-id="e393e-140">From the drop-down, next to Incoming claim type, select **Inside Corporate Network**.</span></span>
   <span data-ttu-id="e393e-141">![Cloud](./media/howto-mfa-adfs/trustedip4.png)</span><span class="sxs-lookup"><span data-stu-id="e393e-141">![Cloud](./media/howto-mfa-adfs/trustedip4.png)</span></span>
8. <span data-ttu-id="e393e-142">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="e393e-142">Click **Finish**.</span></span>
9. <span data-ttu-id="e393e-143">On Issuance Transform Rules, click **Add Rule**.</span><span class="sxs-lookup"><span data-stu-id="e393e-143">On Issuance Transform Rules, click **Add Rule**.</span></span>
10. <span data-ttu-id="e393e-144">On the Add Transform Claim Rule Wizard, select **Send Claims Using a Custom Rule** from the drop-down and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e393e-144">On the Add Transform Claim Rule Wizard, select **Send Claims Using a Custom Rule** from the drop-down and click **Next**.</span></span>
11. <span data-ttu-id="e393e-145">In the box under Claim rule name: enter *Keep Users Signed In*.</span><span class="sxs-lookup"><span data-stu-id="e393e-145">In the box under Claim rule name: enter *Keep Users Signed In*.</span></span>
12. <span data-ttu-id="e393e-146">In the Custom rule box, enter:</span><span class="sxs-lookup"><span data-stu-id="e393e-146">In the Custom rule box, enter:</span></span>

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![Cloud](./media/howto-mfa-adfs/trustedip5.png)
13. <span data-ttu-id="e393e-148">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="e393e-148">Click **Finish**.</span></span>
14. <span data-ttu-id="e393e-149">Click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="e393e-149">Click **Apply**.</span></span>
15. <span data-ttu-id="e393e-150">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="e393e-150">Click **Ok**.</span></span>
16. <span data-ttu-id="e393e-151">Close AD FS Management.</span><span class="sxs-lookup"><span data-stu-id="e393e-151">Close AD FS Management.</span></span>

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a><span data-ttu-id="e393e-152">Configure Azure Multi-Factor Authentication Trusted IPs with Federated Users</span><span class="sxs-lookup"><span data-stu-id="e393e-152">Configure Azure Multi-Factor Authentication Trusted IPs with Federated Users</span></span>

<span data-ttu-id="e393e-153">Now that the claims are in place, we can configure trusted IPs.</span><span class="sxs-lookup"><span data-stu-id="e393e-153">Now that the claims are in place, we can configure trusted IPs.</span></span>

1. <span data-ttu-id="e393e-154">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e393e-154">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e393e-155">Select **Azure Active Directory** > **Conditional access** > **Named locations**.</span><span class="sxs-lookup"><span data-stu-id="e393e-155">Select **Azure Active Directory** > **Conditional access** > **Named locations**.</span></span>
3. <span data-ttu-id="e393e-156">From the **Conditional access - Named locations** blade, select **Configure MFA trusted IPs**</span><span class="sxs-lookup"><span data-stu-id="e393e-156">From the **Conditional access - Named locations** blade, select **Configure MFA trusted IPs**</span></span>

   ![Azure AD conditional access named locations Configure MFA trusted IPs](./media/howto-mfa-adfs/trustedip6.png)

4. <span data-ttu-id="e393e-158">On the Service Settings page, under **trusted IPs**, select **Skip multi-factor-authentication for requests from federated users on my intranet**.</span><span class="sxs-lookup"><span data-stu-id="e393e-158">On the Service Settings page, under **trusted IPs**, select **Skip multi-factor-authentication for requests from federated users on my intranet**.</span></span>  
5. <span data-ttu-id="e393e-159">Click **save**.</span><span class="sxs-lookup"><span data-stu-id="e393e-159">Click **save**.</span></span>

<span data-ttu-id="e393e-160">That’s it!</span><span class="sxs-lookup"><span data-stu-id="e393e-160">That’s it!</span></span> <span data-ttu-id="e393e-161">At this point, federated Office 365 users should only have to use MFA when a claim originates from outside the corporate intranet.</span><span class="sxs-lookup"><span data-stu-id="e393e-161">At this point, federated Office 365 users should only have to use MFA when a claim originates from outside the corporate intranet.</span></span>
