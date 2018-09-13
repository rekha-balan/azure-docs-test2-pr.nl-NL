---
title: Managing custom domain names in your Azure Active Directory | Microsoft Docs
description: Management concepts and how-tos for managing a domain name in Azure Active Directory
services: active-directory
documentationcenter: ''
author: curtand
manager: mtillman
editor: ''
ms.service: active-directory
ms.workload: identity
ms.component: users-groups-roles
ms.topic: article
ms.date: 11/14/2017
ms.author: curtand
ms.reviewer: elkuzmen
ms.openlocfilehash: b503ef4c5cd922d4f7b58940cfc98a83a78ae986
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864883"
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a><span data-ttu-id="0fc3d-103">Managing custom domain names in your Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0fc3d-103">Managing custom domain names in your Azure Active Directory</span></span>
<span data-ttu-id="0fc3d-104">A domain name is an important part of the identifier for many directory resources: it is part of a user name or email address for a user, part of the address for a group, and can be part of the app ID URI for an application.</span><span class="sxs-lookup"><span data-stu-id="0fc3d-104">A domain name is an important part of the identifier for many directory resources: it is part of a user name or email address for a user, part of the address for a group, and can be part of the app ID URI for an application.</span></span> <span data-ttu-id="0fc3d-105">A resource in Azure Active Directory (Azure AD) can include a domain name that is already verified as owned by the directory that contains the resource.</span><span class="sxs-lookup"><span data-stu-id="0fc3d-105">A resource in Azure Active Directory (Azure AD) can include a domain name that is already verified as owned by the directory that contains the resource.</span></span> <span data-ttu-id="0fc3d-106">Only a global administrator can perform domain management tasks in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0fc3d-106">Only a global administrator can perform domain management tasks in Azure AD.</span></span>

## <a name="set-the-primary-domain-name-for-your-azure-ad-directory"></a><span data-ttu-id="0fc3d-107">Set the primary domain name for your Azure AD directory</span><span class="sxs-lookup"><span data-stu-id="0fc3d-107">Set the primary domain name for your Azure AD directory</span></span>
<span data-ttu-id="0fc3d-108">When your directory is created, the initial domain name, such as ‘contoso.onmicrosoft.com,’ is also the primary domain name.</span><span class="sxs-lookup"><span data-stu-id="0fc3d-108">When your directory is created, the initial domain name, such as ‘contoso.onmicrosoft.com,’ is also the primary domain name.</span></span> <span data-ttu-id="0fc3d-109">The primary domain is the default domain name for a new user when you create a new user.</span><span class="sxs-lookup"><span data-stu-id="0fc3d-109">The primary domain is the default domain name for a new user when you create a new user.</span></span> <span data-ttu-id="0fc3d-110">Setting a primary domain name streamlines the process for an administrator to create new users in the portal.</span><span class="sxs-lookup"><span data-stu-id="0fc3d-110">Setting a primary domain name streamlines the process for an administrator to create new users in the portal.</span></span> <span data-ttu-id="0fc3d-111">To change the primary domain name:</span><span class="sxs-lookup"><span data-stu-id="0fc3d-111">To change the primary domain name:</span></span>

1. <span data-ttu-id="0fc3d-112">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span><span class="sxs-lookup"><span data-stu-id="0fc3d-112">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="0fc3d-113">Select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0fc3d-113">Select **Azure Active Directory**.</span></span>
3. <span data-ttu-id="0fc3d-114">Select **Custom domain names**.</span><span class="sxs-lookup"><span data-stu-id="0fc3d-114">Select **Custom domain names**.</span></span>
     
   ![Opening user management](./media/domains-manage/add-custom-domain.png)
4. <span data-ttu-id="0fc3d-116">Select the name of the domain that you want to be the primary domain.</span><span class="sxs-lookup"><span data-stu-id="0fc3d-116">Select the name of the domain that you want to be the primary domain.</span></span>
5. <span data-ttu-id="0fc3d-117">Select the **Make primary** command.</span><span class="sxs-lookup"><span data-stu-id="0fc3d-117">Select the **Make primary** command.</span></span> <span data-ttu-id="0fc3d-118">Confirm your choice when prompted.</span><span class="sxs-lookup"><span data-stu-id="0fc3d-118">Confirm your choice when prompted.</span></span>
   
   ![Make a domain name primary](./media/domains-manage/make-primary-domain.png)

<span data-ttu-id="0fc3d-120">You can change the primary domain name for your directory to be any verified custom domain that is not federated.</span><span class="sxs-lookup"><span data-stu-id="0fc3d-120">You can change the primary domain name for your directory to be any verified custom domain that is not federated.</span></span> <span data-ttu-id="0fc3d-121">Changing the primary domain for your directory will not change the user names for any existing users.</span><span class="sxs-lookup"><span data-stu-id="0fc3d-121">Changing the primary domain for your directory will not change the user names for any existing users.</span></span>

## <a name="add-custom-domain-names-to-your-azure-ad-tenant"></a><span data-ttu-id="0fc3d-122">Add custom domain names to your Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="0fc3d-122">Add custom domain names to your Azure AD tenant</span></span>
<span data-ttu-id="0fc3d-123">You can add up to a maximum of 900 managed domain names.</span><span class="sxs-lookup"><span data-stu-id="0fc3d-123">You can add up to a maximum of 900 managed domain names.</span></span> <span data-ttu-id="0fc3d-124">If you are configuring all your domains for federation with on-premises Active Directory, you can add up to a maximum of 450 domain names in each directory.</span><span class="sxs-lookup"><span data-stu-id="0fc3d-124">If you are configuring all your domains for federation with on-premises Active Directory, you can add up to a maximum of 450 domain names in each directory.</span></span> <span data-ttu-id="0fc3d-125">For more information, see [Federated and managed domain names](https://docs.microsoft.com/azure/active-directory/active-directory-add-domain-concepts#federated-and-managed-domain-names).</span><span class="sxs-lookup"><span data-stu-id="0fc3d-125">For more information, see [Federated and managed domain names](https://docs.microsoft.com/azure/active-directory/active-directory-add-domain-concepts#federated-and-managed-domain-names).</span></span>

## <a name="add-subdomains-of-a-custom-domain"></a><span data-ttu-id="0fc3d-126">Add subdomains of a custom domain</span><span class="sxs-lookup"><span data-stu-id="0fc3d-126">Add subdomains of a custom domain</span></span>
<span data-ttu-id="0fc3d-127">If you want to add a third-level domain name such as ‘europe.contoso.com’ to your directory, you should first add and verify the second-level domain, such as contoso.com.</span><span class="sxs-lookup"><span data-stu-id="0fc3d-127">If you want to add a third-level domain name such as ‘europe.contoso.com’ to your directory, you should first add and verify the second-level domain, such as contoso.com.</span></span> <span data-ttu-id="0fc3d-128">The subdomain will be automatically verified by Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0fc3d-128">The subdomain will be automatically verified by Azure AD.</span></span> <span data-ttu-id="0fc3d-129">To see that the subdomain that you just added has been verified, refresh the page in the browser that lists the domains.</span><span class="sxs-lookup"><span data-stu-id="0fc3d-129">To see that the subdomain that you just added has been verified, refresh the page in the browser that lists the domains.</span></span>

## <a name="what-to-do-if-you-change-the-dns-registrar-for-your-custom-domain-name"></a><span data-ttu-id="0fc3d-130">What to do if you change the DNS registrar for your custom domain name</span><span class="sxs-lookup"><span data-stu-id="0fc3d-130">What to do if you change the DNS registrar for your custom domain name</span></span>
<span data-ttu-id="0fc3d-131">If you change the DNS registrar for your custom domain name, you can continue to use your custom domain name with Azure AD itself without interruption and without additional configuration tasks.</span><span class="sxs-lookup"><span data-stu-id="0fc3d-131">If you change the DNS registrar for your custom domain name, you can continue to use your custom domain name with Azure AD itself without interruption and without additional configuration tasks.</span></span> <span data-ttu-id="0fc3d-132">If you use your custom domain name with Office 365, Intune, or other services that rely on custom domain names in Azure AD, refer to the documentation for those services.</span><span class="sxs-lookup"><span data-stu-id="0fc3d-132">If you use your custom domain name with Office 365, Intune, or other services that rely on custom domain names in Azure AD, refer to the documentation for those services.</span></span>

## <a name="delete-a-custom-domain-name"></a><span data-ttu-id="0fc3d-133">Delete a custom domain name</span><span class="sxs-lookup"><span data-stu-id="0fc3d-133">Delete a custom domain name</span></span>
<span data-ttu-id="0fc3d-134">You can delete a custom domain name from your Azure AD if your organization no longer uses that domain name, or if you need to use that domain name with another Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0fc3d-134">You can delete a custom domain name from your Azure AD if your organization no longer uses that domain name, or if you need to use that domain name with another Azure AD.</span></span>

<span data-ttu-id="0fc3d-135">To delete a custom domain name, you must first ensure that no resources in your directory rely on the domain name.</span><span class="sxs-lookup"><span data-stu-id="0fc3d-135">To delete a custom domain name, you must first ensure that no resources in your directory rely on the domain name.</span></span> <span data-ttu-id="0fc3d-136">You can't delete a domain name from your directory if:</span><span class="sxs-lookup"><span data-stu-id="0fc3d-136">You can't delete a domain name from your directory if:</span></span>

* <span data-ttu-id="0fc3d-137">Any user has a user name, email address, or proxy address that includes the domain name.</span><span class="sxs-lookup"><span data-stu-id="0fc3d-137">Any user has a user name, email address, or proxy address that includes the domain name.</span></span>
* <span data-ttu-id="0fc3d-138">Any group has an email address or proxy address that includes the domain name.</span><span class="sxs-lookup"><span data-stu-id="0fc3d-138">Any group has an email address or proxy address that includes the domain name.</span></span>
* <span data-ttu-id="0fc3d-139">Any application in your Azure AD has an app ID URI that includes the domain name.</span><span class="sxs-lookup"><span data-stu-id="0fc3d-139">Any application in your Azure AD has an app ID URI that includes the domain name.</span></span>

<span data-ttu-id="0fc3d-140">You must change or delete any such resource in your Azure AD directory before you can delete the custom domain name.</span><span class="sxs-lookup"><span data-stu-id="0fc3d-140">You must change or delete any such resource in your Azure AD directory before you can delete the custom domain name.</span></span>

## <a name="use-powershell-or-graph-api-to-manage-domain-names"></a><span data-ttu-id="0fc3d-141">Use PowerShell or Graph API to manage domain names</span><span class="sxs-lookup"><span data-stu-id="0fc3d-141">Use PowerShell or Graph API to manage domain names</span></span>
<span data-ttu-id="0fc3d-142">Most management tasks for domain names in Azure Active Directory can also be completed using Microsoft PowerShell, or programmatically using Azure AD Graph API.</span><span class="sxs-lookup"><span data-stu-id="0fc3d-142">Most management tasks for domain names in Azure Active Directory can also be completed using Microsoft PowerShell, or programmatically using Azure AD Graph API.</span></span>

* [<span data-ttu-id="0fc3d-143">Using PowerShell to manage domain names in Azure AD</span><span class="sxs-lookup"><span data-stu-id="0fc3d-143">Using PowerShell to manage domain names in Azure AD</span></span>](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [<span data-ttu-id="0fc3d-144">Using Graph API to manage domain names in Azure AD</span><span class="sxs-lookup"><span data-stu-id="0fc3d-144">Using Graph API to manage domain names in Azure AD</span></span>](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a><span data-ttu-id="0fc3d-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="0fc3d-145">Next steps</span></span>
* [<span data-ttu-id="0fc3d-146">Add custom domain names</span><span class="sxs-lookup"><span data-stu-id="0fc3d-146">Add custom domain names</span></span>](../fundamentals/add-custom-domain.md)

