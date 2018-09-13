---
title: Managing custom domain names in your Azure Active Directory preview | Microsoft Docs
description: Management concepts and how-tos for managing a domain name in Azure Active Directory
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: 5063cd0a-dba2-4ba9-aa65-b8117490d73a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/12/2016
ms.author: curtand;jeffsta
ms.openlocfilehash: 75b357ef4674ac7c36f6c21ea18dc6e462efaabf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548941"
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory-preview"></a><span data-ttu-id="232ff-103">Managing custom domain names in your Azure Active Directory preview</span><span class="sxs-lookup"><span data-stu-id="232ff-103">Managing custom domain names in your Azure Active Directory preview</span></span>
<span data-ttu-id="232ff-104">A domain name is an important part of the identifier for many directory resources: it is part of a user name or email address for a user, part of the address for a group, and can be part of the app ID URI for an application.</span><span class="sxs-lookup"><span data-stu-id="232ff-104">A domain name is an important part of the identifier for many directory resources: it is part of a user name or email address for a user, part of the address for a group, and can be part of the app ID URI for an application.</span></span> <span data-ttu-id="232ff-105">A resource in Azure Active Directory (Azure AD) preview can include a domain name that is already verified to be owned by the directory that contains the resource.</span><span class="sxs-lookup"><span data-stu-id="232ff-105">A resource in Azure Active Directory (Azure AD) preview can include a domain name that is already verified to be owned by the directory that contains the resource.</span></span> [<span data-ttu-id="232ff-106">What's in the preview?</span><span class="sxs-lookup"><span data-stu-id="232ff-106">What's in the preview?</span></span>](active-directory-preview-explainer.md) <span data-ttu-id="232ff-107">Only a global administrator can perform domain management tasks in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="232ff-107">Only a global administrator can perform domain management tasks in Azure AD.</span></span>

## <a name="set-the-primary-domain-name-for-your-azure-ad-directory"></a><span data-ttu-id="232ff-108">Set the primary domain name for your Azure AD directory</span><span class="sxs-lookup"><span data-stu-id="232ff-108">Set the primary domain name for your Azure AD directory</span></span>
<span data-ttu-id="232ff-109">When your directory is created, the initial domain name, such as ‘contoso.onmicrosoft.com,’ is also the primary domain name.</span><span class="sxs-lookup"><span data-stu-id="232ff-109">When your directory is created, the initial domain name, such as ‘contoso.onmicrosoft.com,’ is also the primary domain name.</span></span> <span data-ttu-id="232ff-110">The primary domain is the default domain name for a new user when you create a new user.</span><span class="sxs-lookup"><span data-stu-id="232ff-110">The primary domain is the default domain name for a new user when you create a new user.</span></span> <span data-ttu-id="232ff-111">This streamlines the process for an administrator to create new users in the portal.</span><span class="sxs-lookup"><span data-stu-id="232ff-111">This streamlines the process for an administrator to create new users in the portal.</span></span> <span data-ttu-id="232ff-112">To change the primary domain name:</span><span class="sxs-lookup"><span data-stu-id="232ff-112">To change the primary domain name:</span></span>

1. <span data-ttu-id="232ff-113">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span><span class="sxs-lookup"><span data-stu-id="232ff-113">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="232ff-114">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span><span class="sxs-lookup"><span data-stu-id="232ff-114">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
   
   ![Opening user management](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-domains-add-azure-portal/user-management.png)
3. <span data-ttu-id="232ff-116">On the ***directory-name*** blade, select **Domain names**.</span><span class="sxs-lookup"><span data-stu-id="232ff-116">On the ***directory-name*** blade, select **Domain names**.</span></span>
4. <span data-ttu-id="232ff-117">On the ***directory-name* - Domain names** blade, select the domain name you would like to make the primary domain name.</span><span class="sxs-lookup"><span data-stu-id="232ff-117">On the ***directory-name* - Domain names** blade, select the domain name you would like to make the primary domain name.</span></span>
5. <span data-ttu-id="232ff-118">On the ***domainname*** blade (that is, the blade that opens that has your new domain name in the title), select the **Make primary** command.</span><span class="sxs-lookup"><span data-stu-id="232ff-118">On the ***domainname*** blade (that is, the blade that opens that has your new domain name in the title), select the **Make primary** command.</span></span> <span data-ttu-id="232ff-119">Confirm your choice when prompted.</span><span class="sxs-lookup"><span data-stu-id="232ff-119">Confirm your choice when prompted.</span></span>
   
   ![Make a domain name primary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-domains-manage-azure-portal/make-primary.png)

<span data-ttu-id="232ff-121">You can change the primary domain name for your directory to be any verified custom domain that is not federated.</span><span class="sxs-lookup"><span data-stu-id="232ff-121">You can change the primary domain name for your directory to be any verified custom domain that is not federated.</span></span> <span data-ttu-id="232ff-122">Changing the primary domain for your directory will not change the user names for any existing users.</span><span class="sxs-lookup"><span data-stu-id="232ff-122">Changing the primary domain for your directory will not change the user names for any existing users.</span></span>

## <a name="add-custom-domain-names-to-your-azure-ad"></a><span data-ttu-id="232ff-123">Add custom domain names to your Azure AD</span><span class="sxs-lookup"><span data-stu-id="232ff-123">Add custom domain names to your Azure AD</span></span>
<span data-ttu-id="232ff-124">You can add up to 900 custom domain names to each Azure AD directory.</span><span class="sxs-lookup"><span data-stu-id="232ff-124">You can add up to 900 custom domain names to each Azure AD directory.</span></span> <span data-ttu-id="232ff-125">The process to [add an additional custom domain name](active-directory-domains-add-azure-portal.md) is the same for the first custom domain name.</span><span class="sxs-lookup"><span data-stu-id="232ff-125">The process to [add an additional custom domain name](active-directory-domains-add-azure-portal.md) is the same for the first custom domain name.</span></span>

## <a name="add-subdomains-of-a-custom-domain"></a><span data-ttu-id="232ff-126">Add subdomains of a custom domain</span><span class="sxs-lookup"><span data-stu-id="232ff-126">Add subdomains of a custom domain</span></span>
<span data-ttu-id="232ff-127">If you want to add a third-level domain name such as ‘europe.contoso.com’ to your directory, you should first add and verify the second-level domain, such as contoso.com.</span><span class="sxs-lookup"><span data-stu-id="232ff-127">If you want to add a third-level domain name such as ‘europe.contoso.com’ to your directory, you should first add and verify the second-level domain, such as contoso.com.</span></span> <span data-ttu-id="232ff-128">The subdomain will be automatically verified by Azure AD.</span><span class="sxs-lookup"><span data-stu-id="232ff-128">The subdomain will be automatically verified by Azure AD.</span></span> <span data-ttu-id="232ff-129">To see that the subdomain that you just added has been verified, refresh the page in the browser that lists the domains.</span><span class="sxs-lookup"><span data-stu-id="232ff-129">To see that the subdomain that you just added has been verified, refresh the page in the browser that lists the domains.</span></span>

## <a name="what-to-do-if-you-change-the-dns-registrar-for-your-custom-domain-name"></a><span data-ttu-id="232ff-130">What to do if you change the DNS registrar for your custom domain name</span><span class="sxs-lookup"><span data-stu-id="232ff-130">What to do if you change the DNS registrar for your custom domain name</span></span>
<span data-ttu-id="232ff-131">If you change the DNS registrar for your custom domain name, you can continue to use your custom domain name with Azure AD itself without interruption and without additional configuration tasks.</span><span class="sxs-lookup"><span data-stu-id="232ff-131">If you change the DNS registrar for your custom domain name, you can continue to use your custom domain name with Azure AD itself without interruption and without additional configuration tasks.</span></span> <span data-ttu-id="232ff-132">If you use your custom domain name with Office 365, Intune, or other services that rely on custom domain names in Azure AD, refer to the documentation for those services.</span><span class="sxs-lookup"><span data-stu-id="232ff-132">If you use your custom domain name with Office 365, Intune, or other services that rely on custom domain names in Azure AD, refer to the documentation for those services.</span></span>

## <a name="delete-a-custom-domain-name"></a><span data-ttu-id="232ff-133">Delete a custom domain name</span><span class="sxs-lookup"><span data-stu-id="232ff-133">Delete a custom domain name</span></span>
<span data-ttu-id="232ff-134">You can delete a custom domain name from your Azure AD if your organization no longer uses that domain name, or if you need to use that domain name with another Azure AD.</span><span class="sxs-lookup"><span data-stu-id="232ff-134">You can delete a custom domain name from your Azure AD if your organization no longer uses that domain name, or if you need to use that domain name with another Azure AD.</span></span>

<span data-ttu-id="232ff-135">To delete a custom domain name, you must first ensure that no resources in your directory rely on the domain name.</span><span class="sxs-lookup"><span data-stu-id="232ff-135">To delete a custom domain name, you must first ensure that no resources in your directory rely on the domain name.</span></span> <span data-ttu-id="232ff-136">You can't delete a domain name from your directory if:</span><span class="sxs-lookup"><span data-stu-id="232ff-136">You can't delete a domain name from your directory if:</span></span>

* <span data-ttu-id="232ff-137">Any user has a user name, email address, or proxy address that includes the domain name.</span><span class="sxs-lookup"><span data-stu-id="232ff-137">Any user has a user name, email address, or proxy address that includes the domain name.</span></span>
* <span data-ttu-id="232ff-138">Any group has an email address or proxy address that includes the domain name.</span><span class="sxs-lookup"><span data-stu-id="232ff-138">Any group has an email address or proxy address that includes the domain name.</span></span>
* <span data-ttu-id="232ff-139">Any application in your Azure AD has an app ID URI that includes the domain name.</span><span class="sxs-lookup"><span data-stu-id="232ff-139">Any application in your Azure AD has an app ID URI that includes the domain name.</span></span>

<span data-ttu-id="232ff-140">You must change or delete any such resource in your Azure AD directory before you can delete the custom domain name.</span><span class="sxs-lookup"><span data-stu-id="232ff-140">You must change or delete any such resource in your Azure AD directory before you can delete the custom domain name.</span></span>

## <a name="use-powershell-or-graph-api-to-manage-domain-names"></a><span data-ttu-id="232ff-141">Use PowerShell or Graph API to manage domain names</span><span class="sxs-lookup"><span data-stu-id="232ff-141">Use PowerShell or Graph API to manage domain names</span></span>
<span data-ttu-id="232ff-142">Most management tasks for domain names in Azure Active Directory can also be completed using Microsoft PowerShell, or programmatically using Azure AD Graph API (in public preview).</span><span class="sxs-lookup"><span data-stu-id="232ff-142">Most management tasks for domain names in Azure Active Directory can also be completed using Microsoft PowerShell, or programmatically using Azure AD Graph API (in public preview).</span></span>

* [<span data-ttu-id="232ff-143">Using PowerShell to manage domain names in Azure AD</span><span class="sxs-lookup"><span data-stu-id="232ff-143">Using PowerShell to manage domain names in Azure AD</span></span>](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [<span data-ttu-id="232ff-144">Using Graph API to manage domain names in Azure AD</span><span class="sxs-lookup"><span data-stu-id="232ff-144">Using Graph API to manage domain names in Azure AD</span></span>](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a><span data-ttu-id="232ff-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="232ff-145">Next steps</span></span>
* [<span data-ttu-id="232ff-146">Add custom domain names</span><span class="sxs-lookup"><span data-stu-id="232ff-146">Add custom domain names</span></span>](active-directory-domains-add-azure-portal.md)



