---
title: Administrator takeover of an unmanaged directory or shadow tenant in Azure Active Directory | Microsoft Docs
description: How to take over a DNS domain name in an unmanaged directory (shadow tenant) in Azure Active Directory.
services: active-directory
documentationcenter: ''
author: curtand
manager: mtillman
editor: ''
ms.service: active-directory
ms.component: users-groups-roles
ms.topic: article
ms.workload: identity
ms.date: 04/06/2017
ms.author: curtand
ms.reviewer: elkuzmen
ms.custom: it-pro
ms.openlocfilehash: 210526e105793820a2e8a80a11b356b1d7d764da
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867388"
---
# <a name="take-over-an-unmanaged-directory-as-administrator-in-azure-active-directory"></a><span data-ttu-id="c35d0-103">Take over an unmanaged directory as administrator in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c35d0-103">Take over an unmanaged directory as administrator in Azure Active Directory</span></span>
<span data-ttu-id="c35d0-104">This article describes two ways to take over a DNS domain name in an unmanaged directory in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c35d0-104">This article describes two ways to take over a DNS domain name in an unmanaged directory in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="c35d0-105">When a self-service user signs up for a cloud service that uses Azure AD, they are added to an unmanaged Azure AD directory based on their email domain.</span><span class="sxs-lookup"><span data-stu-id="c35d0-105">When a self-service user signs up for a cloud service that uses Azure AD, they are added to an unmanaged Azure AD directory based on their email domain.</span></span> <span data-ttu-id="c35d0-106">For more about self-service or "viral" signup for a service, see [What is self-service signup for Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-signup)</span><span class="sxs-lookup"><span data-stu-id="c35d0-106">For more about self-service or "viral" signup for a service, see [What is self-service signup for Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-signup)</span></span>

## <a name="decide-how-you-want-to-take-over-an-unmanaged-directory"></a><span data-ttu-id="c35d0-107">Decide how you want to take over an unmanaged directory</span><span class="sxs-lookup"><span data-stu-id="c35d0-107">Decide how you want to take over an unmanaged directory</span></span>
<span data-ttu-id="c35d0-108">During the process of admin takeover, you can prove ownership as described in [Add a custom domain name to Azure AD](../fundamentals/add-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="c35d0-108">During the process of admin takeover, you can prove ownership as described in [Add a custom domain name to Azure AD](../fundamentals/add-custom-domain.md).</span></span> <span data-ttu-id="c35d0-109">The next sections explain the admin experience in more detail, but here's a summary:</span><span class="sxs-lookup"><span data-stu-id="c35d0-109">The next sections explain the admin experience in more detail, but here's a summary:</span></span>

* <span data-ttu-id="c35d0-110">When you perform an ["internal" admin takeover](#internal-admin-takeover) of an unmanaged Azure directory, you are added as the global administrator of the unmanaged directory.</span><span class="sxs-lookup"><span data-stu-id="c35d0-110">When you perform an ["internal" admin takeover](#internal-admin-takeover) of an unmanaged Azure directory, you are added as the global administrator of the unmanaged directory.</span></span> <span data-ttu-id="c35d0-111">No users, domains, or service plans are migrated to any other directory you administer.</span><span class="sxs-lookup"><span data-stu-id="c35d0-111">No users, domains, or service plans are migrated to any other directory you administer.</span></span>

* <span data-ttu-id="c35d0-112">When you perform an ["external" admin takeover](#external-admin-takeover) of an unmanaged Azure directory, you add the DNS domain name of the unmanaged directory to your managed Azure directory.</span><span class="sxs-lookup"><span data-stu-id="c35d0-112">When you perform an ["external" admin takeover](#external-admin-takeover) of an unmanaged Azure directory, you add the DNS domain name of the unmanaged directory to your managed Azure directory.</span></span> <span data-ttu-id="c35d0-113">When you add the domain name, a mapping of users to resources is created in your managed Azure directory so that users can continue to access services without interruption.</span><span class="sxs-lookup"><span data-stu-id="c35d0-113">When you add the domain name, a mapping of users to resources is created in your managed Azure directory so that users can continue to access services without interruption.</span></span> 

## <a name="internal-admin-takeover"></a><span data-ttu-id="c35d0-114">Internal admin takeover</span><span class="sxs-lookup"><span data-stu-id="c35d0-114">Internal admin takeover</span></span>

<span data-ttu-id="c35d0-115">Some products that include SharePoint and OneDrive, such as Office 365, do not support external takeover.</span><span class="sxs-lookup"><span data-stu-id="c35d0-115">Some products that include SharePoint and OneDrive, such as Office 365, do not support external takeover.</span></span> <span data-ttu-id="c35d0-116">If that is your scenario, or if you are an admin and want to take over an unmanaged or "shadow" tenant create by users who used self-service sign-up, you can do this with an internal admin takeover.</span><span class="sxs-lookup"><span data-stu-id="c35d0-116">If that is your scenario, or if you are an admin and want to take over an unmanaged or "shadow" tenant create by users who used self-service sign-up, you can do this with an internal admin takeover.</span></span>

1. <span data-ttu-id="c35d0-117">Create a user context in the unmanaged tenant through signing up with such as Power BI.</span><span class="sxs-lookup"><span data-stu-id="c35d0-117">Create a user context in the unmanaged tenant through signing up with such as Power BI.</span></span> <span data-ttu-id="c35d0-118">For convenience of example, these steps assume that path.</span><span class="sxs-lookup"><span data-stu-id="c35d0-118">For convenience of example, these steps assume that path.</span></span>

2. <span data-ttu-id="c35d0-119">Open the [Power BI site](https://powerbi.com) and select **Start Free**.</span><span class="sxs-lookup"><span data-stu-id="c35d0-119">Open the [Power BI site](https://powerbi.com) and select **Start Free**.</span></span> <span data-ttu-id="c35d0-120">Enter a user account that uses the domain name for the organization; for example, `admin@fourthcoffee.xyz`.</span><span class="sxs-lookup"><span data-stu-id="c35d0-120">Enter a user account that uses the domain name for the organization; for example, `admin@fourthcoffee.xyz`.</span></span> <span data-ttu-id="c35d0-121">After you enter in the verification code, check your email for the confirmation code.</span><span class="sxs-lookup"><span data-stu-id="c35d0-121">After you enter in the verification code, check your email for the confirmation code.</span></span>

3. <span data-ttu-id="c35d0-122">In the confirmation email from Power BI, select **Yes, that's me**.</span><span class="sxs-lookup"><span data-stu-id="c35d0-122">In the confirmation email from Power BI, select **Yes, that's me**.</span></span>

4. <span data-ttu-id="c35d0-123">Sign in to the [Office 365 Admin center](https://portal.office.com/adminportal/Home) with the Power BI user account.</span><span class="sxs-lookup"><span data-stu-id="c35d0-123">Sign in to the [Office 365 Admin center](https://portal.office.com/adminportal/Home) with the Power BI user account.</span></span> <span data-ttu-id="c35d0-124">You receive a message that instructs you to **Become the Admin** of the domain name that was already verified in the unmanaged tenant.</span><span class="sxs-lookup"><span data-stu-id="c35d0-124">You receive a message that instructs you to **Become the Admin** of the domain name that was already verified in the unmanaged tenant.</span></span> <span data-ttu-id="c35d0-125">select **Yes, I want to be the admin**.</span><span class="sxs-lookup"><span data-stu-id="c35d0-125">select **Yes, I want to be the admin**.</span></span>
  
  ![first screenshot for Become the Admin](./media/domains-admin-takeover/become-admin-first.png)
  
5. <span data-ttu-id="c35d0-127">Add the TXT record to prove that you own the domain name **fourthcoffee.xyz** at your domain name registrar.</span><span class="sxs-lookup"><span data-stu-id="c35d0-127">Add the TXT record to prove that you own the domain name **fourthcoffee.xyz** at your domain name registrar.</span></span> <span data-ttu-id="c35d0-128">In this example, it is GoDaddy.com.</span><span class="sxs-lookup"><span data-stu-id="c35d0-128">In this example, it is GoDaddy.com.</span></span>
  
  ![Add a txt record for the domain name](./media/domains-admin-takeover/become-admin-txt-record.png)

<span data-ttu-id="c35d0-130">When the DNS TXT records are verified at your domain name registrar, you can manage the Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="c35d0-130">When the DNS TXT records are verified at your domain name registrar, you can manage the Azure AD tenant.</span></span>

<span data-ttu-id="c35d0-131">When you complete the preceding steps, you are now the global administrator of the Fourth Coffee tenant in Office 365.</span><span class="sxs-lookup"><span data-stu-id="c35d0-131">When you complete the preceding steps, you are now the global administrator of the Fourth Coffee tenant in Office 365.</span></span> <span data-ttu-id="c35d0-132">To integrate the domain name with your other Azure services, you can remove it from Office 365 and add it to a different managed tenant in Azure.</span><span class="sxs-lookup"><span data-stu-id="c35d0-132">To integrate the domain name with your other Azure services, you can remove it from Office 365 and add it to a different managed tenant in Azure.</span></span>

### <a name="adding-the-domain-name-to-a-managed-tenant-in-azure-ad"></a><span data-ttu-id="c35d0-133">Adding the domain name to a managed tenant in Azure AD</span><span class="sxs-lookup"><span data-stu-id="c35d0-133">Adding the domain name to a managed tenant in Azure AD</span></span> 

1. <span data-ttu-id="c35d0-134">Open the [Office 365 Admin center](https://portal.office.com/adminportal/Home).</span><span class="sxs-lookup"><span data-stu-id="c35d0-134">Open the [Office 365 Admin center](https://portal.office.com/adminportal/Home).</span></span>
2. <span data-ttu-id="c35d0-135">Select **Users** tab, and create a new user account with a name like *user@fourthcoffeexyz.onmicrosoft.com* that does not use the custom domain name.</span><span class="sxs-lookup"><span data-stu-id="c35d0-135">Select **Users** tab, and create a new user account with a name like *user@fourthcoffeexyz.onmicrosoft.com* that does not use the custom domain name.</span></span> 
3. <span data-ttu-id="c35d0-136">Ensure that the new user account has global admin privileges for the Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="c35d0-136">Ensure that the new user account has global admin privileges for the Azure AD tenant.</span></span>
4. <span data-ttu-id="c35d0-137">Open **Domains** tab in the Office 365 Admin center, select the domain name and select **Remove**.</span><span class="sxs-lookup"><span data-stu-id="c35d0-137">Open **Domains** tab in the Office 365 Admin center, select the domain name and select **Remove**.</span></span> 
  
  ![remove the domain name from Office 365](./media/domains-admin-takeover/remove-domain-from-o365.png)
  
5. <span data-ttu-id="c35d0-139">If you have any users or groups in Office 365 that reference the removed domain name, they must be renamed to the .onmicrosoft.com domain.</span><span class="sxs-lookup"><span data-stu-id="c35d0-139">If you have any users or groups in Office 365 that reference the removed domain name, they must be renamed to the .onmicrosoft.com domain.</span></span> <span data-ttu-id="c35d0-140">If you force delete the domain name, all users are automatically renamed, in this example to *user@fourthcoffeexyz.onmicrosoft.com*.</span><span class="sxs-lookup"><span data-stu-id="c35d0-140">If you force delete the domain name, all users are automatically renamed, in this example to *user@fourthcoffeexyz.onmicrosoft.com*.</span></span>
  
6. <span data-ttu-id="c35d0-141">Sign in to the [Azure AD admin center](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) with an account that is the global admin for the Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="c35d0-141">Sign in to the [Azure AD admin center](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) with an account that is the global admin for the Azure AD tenant.</span></span>
  
7. <span data-ttu-id="c35d0-142">Select **Custom domain names**, then add the domain name.</span><span class="sxs-lookup"><span data-stu-id="c35d0-142">Select **Custom domain names**, then add the domain name.</span></span> <span data-ttu-id="c35d0-143">You'll have to enter the DNS TXT records to verify ownership of the domain name.</span><span class="sxs-lookup"><span data-stu-id="c35d0-143">You'll have to enter the DNS TXT records to verify ownership of the domain name.</span></span> 
  
  ![domain added to Azure AD](./media/domains-admin-takeover/add-domain-to-azure-ad.png)
  
> [!NOTE]
> <span data-ttu-id="c35d0-145">Any users of Power BI or Azure Rights Management service who have licenses assigned in the Office 365 tenant must save their dashboards if the domain name is removed.</span><span class="sxs-lookup"><span data-stu-id="c35d0-145">Any users of Power BI or Azure Rights Management service who have licenses assigned in the Office 365 tenant must save their dashboards if the domain name is removed.</span></span> <span data-ttu-id="c35d0-146">They must sign in with a user name like *user@fourthcoffeexyz.onmicrosoft.com* rather than *user@fourthcoffee.xyz*.</span><span class="sxs-lookup"><span data-stu-id="c35d0-146">They must sign in with a user name like *user@fourthcoffeexyz.onmicrosoft.com* rather than *user@fourthcoffee.xyz*.</span></span>

## <a name="external-admin-takeover"></a><span data-ttu-id="c35d0-147">External admin takeover</span><span class="sxs-lookup"><span data-stu-id="c35d0-147">External admin takeover</span></span>

<span data-ttu-id="c35d0-148">If you already manage a tenant with Azure services or Office 365, you cannot add a custom domain name if it is already verified in another Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="c35d0-148">If you already manage a tenant with Azure services or Office 365, you cannot add a custom domain name if it is already verified in another Azure AD tenant.</span></span> <span data-ttu-id="c35d0-149">However, from your managed tenant in Azure AD you can take over an unmanaged tenant as an external admin takeover.</span><span class="sxs-lookup"><span data-stu-id="c35d0-149">However, from your managed tenant in Azure AD you can take over an unmanaged tenant as an external admin takeover.</span></span> <span data-ttu-id="c35d0-150">The general procedure follows the article [Add a custom domain to Azure AD](../fundamentals/add-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="c35d0-150">The general procedure follows the article [Add a custom domain to Azure AD](../fundamentals/add-custom-domain.md).</span></span>

<span data-ttu-id="c35d0-151">When you verify ownership of the domain name, Azure AD removes the domain name from the unmanaged tenant and moves it to your existing tenant.</span><span class="sxs-lookup"><span data-stu-id="c35d0-151">When you verify ownership of the domain name, Azure AD removes the domain name from the unmanaged tenant and moves it to your existing tenant.</span></span> <span data-ttu-id="c35d0-152">External admin takeover of an unmanaged directory requires the same DNS TXT validation process as internal admin takeover.</span><span class="sxs-lookup"><span data-stu-id="c35d0-152">External admin takeover of an unmanaged directory requires the same DNS TXT validation process as internal admin takeover.</span></span> <span data-ttu-id="c35d0-153">The difference is that the following are also moved over with the domain name:</span><span class="sxs-lookup"><span data-stu-id="c35d0-153">The difference is that the following are also moved over with the domain name:</span></span>

- <span data-ttu-id="c35d0-154">Users</span><span class="sxs-lookup"><span data-stu-id="c35d0-154">Users</span></span>
- <span data-ttu-id="c35d0-155">Subscriptions</span><span class="sxs-lookup"><span data-stu-id="c35d0-155">Subscriptions</span></span>
- <span data-ttu-id="c35d0-156">License assignments</span><span class="sxs-lookup"><span data-stu-id="c35d0-156">License assignments</span></span>

### <a name="support-for-external-admin-takeover"></a><span data-ttu-id="c35d0-157">Support for external admin takeover</span><span class="sxs-lookup"><span data-stu-id="c35d0-157">Support for external admin takeover</span></span>
<span data-ttu-id="c35d0-158">External admin takeover is supported by the following online services:</span><span class="sxs-lookup"><span data-stu-id="c35d0-158">External admin takeover is supported by the following online services:</span></span>

- <span data-ttu-id="c35d0-159">Power BI</span><span class="sxs-lookup"><span data-stu-id="c35d0-159">Power BI</span></span>
- <span data-ttu-id="c35d0-160">Azure Rights Management</span><span class="sxs-lookup"><span data-stu-id="c35d0-160">Azure Rights Management</span></span>
- <span data-ttu-id="c35d0-161">Exchange Online</span><span class="sxs-lookup"><span data-stu-id="c35d0-161">Exchange Online</span></span>

<span data-ttu-id="c35d0-162">The supported service plans include:</span><span class="sxs-lookup"><span data-stu-id="c35d0-162">The supported service plans include:</span></span>

- <span data-ttu-id="c35d0-163">Power BI Free</span><span class="sxs-lookup"><span data-stu-id="c35d0-163">Power BI Free</span></span>
- <span data-ttu-id="c35d0-164">Power BI Pro</span><span class="sxs-lookup"><span data-stu-id="c35d0-164">Power BI Pro</span></span>
- <span data-ttu-id="c35d0-165">PowerApps Free</span><span class="sxs-lookup"><span data-stu-id="c35d0-165">PowerApps Free</span></span>
- <span data-ttu-id="c35d0-166">PowerFlow Free</span><span class="sxs-lookup"><span data-stu-id="c35d0-166">PowerFlow Free</span></span>
- <span data-ttu-id="c35d0-167">RMS for individuals</span><span class="sxs-lookup"><span data-stu-id="c35d0-167">RMS for individuals</span></span>
- <span data-ttu-id="c35d0-168">Microsoft Stream</span><span class="sxs-lookup"><span data-stu-id="c35d0-168">Microsoft Stream</span></span>
- <span data-ttu-id="c35d0-169">Dynamics 365 free trial</span><span class="sxs-lookup"><span data-stu-id="c35d0-169">Dynamics 365 free trial</span></span>

<span data-ttu-id="c35d0-170">External admin takeover is not supported for any service that has service plans that include SharePoint, OneDrive, or Skype For Business; for example, through an Office free subscription or the Office Basic SKU.</span><span class="sxs-lookup"><span data-stu-id="c35d0-170">External admin takeover is not supported for any service that has service plans that include SharePoint, OneDrive, or Skype For Business; for example, through an Office free subscription or the Office Basic SKU.</span></span> <span data-ttu-id="c35d0-171">You can optionally use the [**ForceTakeover** option](#azure-ad-powershell-cmdlets-for-the-forcetakeover-option) for removing the domain name from the unmanaged tenant and verifying it on the desired tenant.</span><span class="sxs-lookup"><span data-stu-id="c35d0-171">You can optionally use the [**ForceTakeover** option](#azure-ad-powershell-cmdlets-for-the-forcetakeover-option) for removing the domain name from the unmanaged tenant and verifying it on the desired tenant.</span></span> <span data-ttu-id="c35d0-172">This ForceTakeover option will not move over users, or retain access to the subscription.</span><span class="sxs-lookup"><span data-stu-id="c35d0-172">This ForceTakeover option will not move over users, or retain access to the subscription.</span></span> <span data-ttu-id="c35d0-173">Instead, this option only moves the domain name.</span><span class="sxs-lookup"><span data-stu-id="c35d0-173">Instead, this option only moves the domain name.</span></span> 

#### <a name="more-information-about-rms-for-individuals"></a><span data-ttu-id="c35d0-174">More information about RMS for individuals</span><span class="sxs-lookup"><span data-stu-id="c35d0-174">More information about RMS for individuals</span></span>

<span data-ttu-id="c35d0-175">For [RMS for individuals](/azure/information-protection/rms-for-individuals), when the unmanaged tenant is in the same region as the tenant that you own, the automatically created [Azure Information Protection tenant key](/azure/information-protection/plan-implement-tenant-key) and [default protection templates](/azure/information-protection/configure-usage-rights#rights-included-in-the-default-templates) are additionally moved over with the domain name.</span><span class="sxs-lookup"><span data-stu-id="c35d0-175">For [RMS for individuals](/azure/information-protection/rms-for-individuals), when the unmanaged tenant is in the same region as the tenant that you own, the automatically created [Azure Information Protection tenant key](/azure/information-protection/plan-implement-tenant-key) and [default protection templates](/azure/information-protection/configure-usage-rights#rights-included-in-the-default-templates) are additionally moved over with the domain name.</span></span> 

<span data-ttu-id="c35d0-176">The key and templates are not moved over when the unmanaged tenant is in a different region.</span><span class="sxs-lookup"><span data-stu-id="c35d0-176">The key and templates are not moved over when the unmanaged tenant is in a different region.</span></span> <span data-ttu-id="c35d0-177">For example, the unmanaged tenant is in Europe and the tenant you own is in North American.</span><span class="sxs-lookup"><span data-stu-id="c35d0-177">For example, the unmanaged tenant is in Europe and the tenant you own is in North American.</span></span> 

<span data-ttu-id="c35d0-178">Although RMS for individuals is designed to support Azure AD authentication to open protected content, it doesn't prevent users from also protecting content.</span><span class="sxs-lookup"><span data-stu-id="c35d0-178">Although RMS for individuals is designed to support Azure AD authentication to open protected content, it doesn't prevent users from also protecting content.</span></span> <span data-ttu-id="c35d0-179">If users did protect content with the RMS for individuals subscription, and the key and templates were not moved over, that content will not be accessible after the domain takeover.</span><span class="sxs-lookup"><span data-stu-id="c35d0-179">If users did protect content with the RMS for individuals subscription, and the key and templates were not moved over, that content will not be accessible after the domain takeover.</span></span>    

### <a name="azure-ad-powershell-cmdlets-for-the-forcetakeover-option"></a><span data-ttu-id="c35d0-180">Azure AD PowerShell cmdlets for the ForceTakeover option</span><span class="sxs-lookup"><span data-stu-id="c35d0-180">Azure AD PowerShell cmdlets for the ForceTakeover option</span></span>
<span data-ttu-id="c35d0-181">You can see these cmdlets used in [PowerShell example](#powershell-example).</span><span class="sxs-lookup"><span data-stu-id="c35d0-181">You can see these cmdlets used in [PowerShell example](#powershell-example).</span></span>


<span data-ttu-id="c35d0-182">cmdlet</span><span class="sxs-lookup"><span data-stu-id="c35d0-182">cmdlet</span></span> | <span data-ttu-id="c35d0-183">Usage</span><span class="sxs-lookup"><span data-stu-id="c35d0-183">Usage</span></span> 
------- | -------
`connect-msolservice` | <span data-ttu-id="c35d0-184">When prompted, sign in to your managed tenant.</span><span class="sxs-lookup"><span data-stu-id="c35d0-184">When prompted, sign in to your managed tenant.</span></span>
`get-msoldomain` | <span data-ttu-id="c35d0-185">Shows your domain names associated with the current tenant.</span><span class="sxs-lookup"><span data-stu-id="c35d0-185">Shows your domain names associated with the current tenant.</span></span>
`new-msoldomain –name <domainname>` | <span data-ttu-id="c35d0-186">Adds the domain name to tenant as Unverified (no DNS verification has been performed yet).</span><span class="sxs-lookup"><span data-stu-id="c35d0-186">Adds the domain name to tenant as Unverified (no DNS verification has been performed yet).</span></span>
`get-msoldomain` | <span data-ttu-id="c35d0-187">The domain name is now included in the list of domain names associated with your managed tenant, but is listed as **Unverified**.</span><span class="sxs-lookup"><span data-stu-id="c35d0-187">The domain name is now included in the list of domain names associated with your managed tenant, but is listed as **Unverified**.</span></span>
`get-msoldomainverificationdns –Domainname <domainname> –Mode DnsTxtRecord` | <span data-ttu-id="c35d0-188">Provides the information to put into new DNS TXT record for the domain (MS=xxxxx).</span><span class="sxs-lookup"><span data-stu-id="c35d0-188">Provides the information to put into new DNS TXT record for the domain (MS=xxxxx).</span></span> <span data-ttu-id="c35d0-189">Verification might not happen immediately because it takes some time for the TXT record to propagate, so wait a few minutes before considering the **-ForceTakeover** option.</span><span class="sxs-lookup"><span data-stu-id="c35d0-189">Verification might not happen immediately because it takes some time for the TXT record to propagate, so wait a few minutes before considering the **-ForceTakeover** option.</span></span> 
`confirm-msoldomain –Domainname <domainname> –ForceTakeover Force` | <li><span data-ttu-id="c35d0-190">If your domain name is still not verified, you can proceed with the **-ForceTakeover** option.</span><span class="sxs-lookup"><span data-stu-id="c35d0-190">If your domain name is still not verified, you can proceed with the **-ForceTakeover** option.</span></span> <span data-ttu-id="c35d0-191">It verifies that the TXT record was created and kicks off the takeover process.</span><span class="sxs-lookup"><span data-stu-id="c35d0-191">It verifies that the TXT record was created and kicks off the takeover process.</span></span><li><span data-ttu-id="c35d0-192">The **-ForceTakeover** option should be added to the cmdlet only when forcing an external admin takeover, such as when the unmanaged tenant has Office 365 services blocking the takeover.</span><span class="sxs-lookup"><span data-stu-id="c35d0-192">The **-ForceTakeover** option should be added to the cmdlet only when forcing an external admin takeover, such as when the unmanaged tenant has Office 365 services blocking the takeover.</span></span>
`get-msoldomain` | <span data-ttu-id="c35d0-193">The domain list now shows the domain name as **Verified**.</span><span class="sxs-lookup"><span data-stu-id="c35d0-193">The domain list now shows the domain name as **Verified**.</span></span>

### <a name="powershell-example"></a><span data-ttu-id="c35d0-194">PowerShell example</span><span class="sxs-lookup"><span data-stu-id="c35d0-194">PowerShell example</span></span>

1. <span data-ttu-id="c35d0-195">Connect to Azure AD using the credentials that were used to respond to the self-service offering:</span><span class="sxs-lookup"><span data-stu-id="c35d0-195">Connect to Azure AD using the credentials that were used to respond to the self-service offering:</span></span>
  ````
    import-module MSOnline
    $msolcred = get-credential
    
    connect-msolservice -credential $msolcred
  ````
2. <span data-ttu-id="c35d0-196">Get a list of domains:</span><span class="sxs-lookup"><span data-stu-id="c35d0-196">Get a list of domains:</span></span>
  
  ````
    Get-MsolDomain
  ````
3. <span data-ttu-id="c35d0-197">Run the Get-MsolDomainVerificationDns cmdlet to create a challenge:</span><span class="sxs-lookup"><span data-stu-id="c35d0-197">Run the Get-MsolDomainVerificationDns cmdlet to create a challenge:</span></span>
  ````
    Get-MsolDomainVerificationDns –DomainName *your_domain_name* –Mode DnsTxtRecord
  
    For example:
  
    Get-MsolDomainVerificationDns –DomainName contoso.com –Mode DnsTxtRecord
  ````

4. <span data-ttu-id="c35d0-198">Copy the value (the challenge) that is returned from this command.</span><span class="sxs-lookup"><span data-stu-id="c35d0-198">Copy the value (the challenge) that is returned from this command.</span></span> <span data-ttu-id="c35d0-199">For example:</span><span class="sxs-lookup"><span data-stu-id="c35d0-199">For example:</span></span>
  ````
    MS=32DD01B82C05D27151EA9AE93C5890787F0E65D9
  ````
5. <span data-ttu-id="c35d0-200">In your public DNS namespace, create a DNS txt record that contains the value that you copied in the previous step.</span><span class="sxs-lookup"><span data-stu-id="c35d0-200">In your public DNS namespace, create a DNS txt record that contains the value that you copied in the previous step.</span></span> <span data-ttu-id="c35d0-201">The name for this record is the name of the parent domain, so if you create this resource record by using the DNS role from Windows Server, leave the Record name blank and just paste the value into the Text box.</span><span class="sxs-lookup"><span data-stu-id="c35d0-201">The name for this record is the name of the parent domain, so if you create this resource record by using the DNS role from Windows Server, leave the Record name blank and just paste the value into the Text box.</span></span>
6. <span data-ttu-id="c35d0-202">Run the Confirm-MsolDomain cmdlet to verify the challenge:</span><span class="sxs-lookup"><span data-stu-id="c35d0-202">Run the Confirm-MsolDomain cmdlet to verify the challenge:</span></span>
  
  ````
    Confirm-MsolEmailVerifiedDomain -DomainName *your_domain_name*
  ````
  
  <span data-ttu-id="c35d0-203">For example:</span><span class="sxs-lookup"><span data-stu-id="c35d0-203">For example:</span></span>
  
  ````
    Confirm-MsolEmailVerifiedDomain -DomainName contoso.com
  ````

<span data-ttu-id="c35d0-204">A successful challenge returns you to the prompt without an error.</span><span class="sxs-lookup"><span data-stu-id="c35d0-204">A successful challenge returns you to the prompt without an error.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c35d0-205">Next steps</span><span class="sxs-lookup"><span data-stu-id="c35d0-205">Next steps</span></span>
* [<span data-ttu-id="c35d0-206">Add a custom domain name to Azure AD</span><span class="sxs-lookup"><span data-stu-id="c35d0-206">Add a custom domain name to Azure AD</span></span>](../fundamentals/add-custom-domain.md)
* [<span data-ttu-id="c35d0-207">How to install and configure Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c35d0-207">How to install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="c35d0-208">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c35d0-208">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="c35d0-209">Azure Cmdlet Reference</span><span class="sxs-lookup"><span data-stu-id="c35d0-209">Azure Cmdlet Reference</span></span>](/powershell/azure/get-started-azureps)
* [<span data-ttu-id="c35d0-210">Set-MsolCompanySettings</span><span class="sxs-lookup"><span data-stu-id="c35d0-210">Set-MsolCompanySettings</span></span>](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0)

<!--Image references-->
[1]: ./media/active-directory-self-service-signup/SelfServiceSignUpControls.png
