---
title: Managing custom domain names in your Azure Active Directory | Microsoft Docs
description: Management concepts and how-tos for managing a custom domain in Azure Active Directory
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: cf3523bd-9ee0-439e-963d-ccea038867b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: curtand;jeffsta
ms.openlocfilehash: a0984c20bac95aeb7b21fba836f567c8dd1fe044
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550582"
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a><span data-ttu-id="2c17f-103">Managing custom domain names in your Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2c17f-103">Managing custom domain names in your Azure Active Directory</span></span>
<span data-ttu-id="2c17f-104">A domain name is an important part of the identifier for many directory resources: it is part of a user name or email address for a user, part of the address for a group, and can be part of the app ID URI for an application.</span><span class="sxs-lookup"><span data-stu-id="2c17f-104">A domain name is an important part of the identifier for many directory resources: it is part of a user name or email address for a user, part of the address for a group, and can be part of the app ID URI for an application.</span></span> <span data-ttu-id="2c17f-105">A resource in Azure Active Directory (Azure AD) can include a domain name that is already verified to be owned by the directory that contains the resource.</span><span class="sxs-lookup"><span data-stu-id="2c17f-105">A resource in Azure Active Directory (Azure AD) can include a domain name that is already verified to be owned by the directory that contains the resource.</span></span> <span data-ttu-id="2c17f-106">Only a global administrator can perform domain management tasks in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2c17f-106">Only a global administrator can perform domain management tasks in Azure AD.</span></span>

## <a name="set-the-primary-domain-name-for-your-azure-ad-directory"></a><span data-ttu-id="2c17f-107">Set the primary domain name for your Azure AD directory</span><span class="sxs-lookup"><span data-stu-id="2c17f-107">Set the primary domain name for your Azure AD directory</span></span>
<span data-ttu-id="2c17f-108">When your directory is created, the initial domain name, such as ‘contoso.onmicrosoft.com,’ is also the primary domain name for your directory.</span><span class="sxs-lookup"><span data-stu-id="2c17f-108">When your directory is created, the initial domain name, such as ‘contoso.onmicrosoft.com,’ is also the primary domain name for your directory.</span></span> <span data-ttu-id="2c17f-109">The primary domain is the default domain name for a new user when you create a new user in the [Azure classic portal](https://manage.windowsazure.com/), or other portals such as the Office 365 admin portal.</span><span class="sxs-lookup"><span data-stu-id="2c17f-109">The primary domain is the default domain name for a new user when you create a new user in the [Azure classic portal](https://manage.windowsazure.com/), or other portals such as the Office 365 admin portal.</span></span> <span data-ttu-id="2c17f-110">This streamlines the process for an administrator to create new users in the portal.</span><span class="sxs-lookup"><span data-stu-id="2c17f-110">This streamlines the process for an administrator to create new users in the portal.</span></span>

<span data-ttu-id="2c17f-111">To change the primary domain name for your directory:</span><span class="sxs-lookup"><span data-stu-id="2c17f-111">To change the primary domain name for your directory:</span></span>

1. <span data-ttu-id="2c17f-112">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) with a user account that is a global administrator of your Azure AD directory.</span><span class="sxs-lookup"><span data-stu-id="2c17f-112">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) with a user account that is a global administrator of your Azure AD directory.</span></span>
2. <span data-ttu-id="2c17f-113">Select **Active Directory** on the left navigation bar.</span><span class="sxs-lookup"><span data-stu-id="2c17f-113">Select **Active Directory** on the left navigation bar.</span></span>
3. <span data-ttu-id="2c17f-114">Open your directory.</span><span class="sxs-lookup"><span data-stu-id="2c17f-114">Open your directory.</span></span>
4. <span data-ttu-id="2c17f-115">Select the **Domains** tab.</span><span class="sxs-lookup"><span data-stu-id="2c17f-115">Select the **Domains** tab.</span></span>
5. <span data-ttu-id="2c17f-116">Select the **Change primary** button on the command bar.</span><span class="sxs-lookup"><span data-stu-id="2c17f-116">Select the **Change primary** button on the command bar.</span></span>
6. <span data-ttu-id="2c17f-117">Select the domain that you want to be the new primary domain for your directory.</span><span class="sxs-lookup"><span data-stu-id="2c17f-117">Select the domain that you want to be the new primary domain for your directory.</span></span>

<span data-ttu-id="2c17f-118">You can change the primary domain name for your directory to be any verified custom domain that is not federated.</span><span class="sxs-lookup"><span data-stu-id="2c17f-118">You can change the primary domain name for your directory to be any verified custom domain that is not federated.</span></span> <span data-ttu-id="2c17f-119">Changing the primary domain for your directory will not change the user names for any existing users.</span><span class="sxs-lookup"><span data-stu-id="2c17f-119">Changing the primary domain for your directory will not change the user names for any existing users.</span></span>

## <a name="add-custom-domain-names-to-your-azure-ad"></a><span data-ttu-id="2c17f-120">Add custom domain names to your Azure AD</span><span class="sxs-lookup"><span data-stu-id="2c17f-120">Add custom domain names to your Azure AD</span></span>
<span data-ttu-id="2c17f-121">You can add up to 900 custom domain names to each Azure AD directory.</span><span class="sxs-lookup"><span data-stu-id="2c17f-121">You can add up to 900 custom domain names to each Azure AD directory.</span></span> <span data-ttu-id="2c17f-122">The process to [add an additional custom domain name](active-directory-add-domain.md) is the same for the first custom domain name.</span><span class="sxs-lookup"><span data-stu-id="2c17f-122">The process to [add an additional custom domain name](active-directory-add-domain.md) is the same for the first custom domain name.</span></span>

## <a name="add-subdomains-of-a-custom-domain"></a><span data-ttu-id="2c17f-123">Add subdomains of a custom domain</span><span class="sxs-lookup"><span data-stu-id="2c17f-123">Add subdomains of a custom domain</span></span>
<span data-ttu-id="2c17f-124">If you want to add a third-level domain name such as ‘europe.contoso.com’ to your directory, you should first add and verify the second-level domain, such as contoso.com.</span><span class="sxs-lookup"><span data-stu-id="2c17f-124">If you want to add a third-level domain name such as ‘europe.contoso.com’ to your directory, you should first add and verify the second-level domain, such as contoso.com.</span></span> <span data-ttu-id="2c17f-125">The subdomain will be automatically verified by Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2c17f-125">The subdomain will be automatically verified by Azure AD.</span></span> <span data-ttu-id="2c17f-126">To see that the subdomain that you just added has been verified, refresh the page in the browser that lists the domains in your directory.</span><span class="sxs-lookup"><span data-stu-id="2c17f-126">To see that the subdomain that you just added has been verified, refresh the page in the browser that lists the domains in your directory.</span></span>

## <a name="what-to-do-if-you-change-the-dns-registrar-for-your-custom-domain-name"></a><span data-ttu-id="2c17f-127">What to do if you change the DNS registrar for your custom domain name</span><span class="sxs-lookup"><span data-stu-id="2c17f-127">What to do if you change the DNS registrar for your custom domain name</span></span>
<span data-ttu-id="2c17f-128">If you change the DNS registrar for your custom domain name, you can continue to use your custom domain name with Azure AD itself without interruption and without additional configuration tasks.</span><span class="sxs-lookup"><span data-stu-id="2c17f-128">If you change the DNS registrar for your custom domain name, you can continue to use your custom domain name with Azure AD itself without interruption and without additional configuration tasks.</span></span> <span data-ttu-id="2c17f-129">If you use your custom domain name with Office 365, Intune, or other services that rely on custom domain names in Azure AD, refer to the documentation for those services.</span><span class="sxs-lookup"><span data-stu-id="2c17f-129">If you use your custom domain name with Office 365, Intune, or other services that rely on custom domain names in Azure AD, refer to the documentation for those services.</span></span>

## <a name="delete-a-custom-domain-name"></a><span data-ttu-id="2c17f-130">Delete a custom domain name</span><span class="sxs-lookup"><span data-stu-id="2c17f-130">Delete a custom domain name</span></span>
<span data-ttu-id="2c17f-131">You can delete a custom domain name from your Azure AD if your organization no longer uses that domain name, or if you need to use that domain name with another Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2c17f-131">You can delete a custom domain name from your Azure AD if your organization no longer uses that domain name, or if you need to use that domain name with another Azure AD.</span></span>

<span data-ttu-id="2c17f-132">To delete a custom domain name, you must first ensure that no resources in your directory rely on the domain name.</span><span class="sxs-lookup"><span data-stu-id="2c17f-132">To delete a custom domain name, you must first ensure that no resources in your directory rely on the domain name.</span></span> <span data-ttu-id="2c17f-133">You can't delete a domain name from your directory if:</span><span class="sxs-lookup"><span data-stu-id="2c17f-133">You can't delete a domain name from your directory if:</span></span>

* <span data-ttu-id="2c17f-134">Any user has a user name, email address, or proxy address that include the domain name.</span><span class="sxs-lookup"><span data-stu-id="2c17f-134">Any user has a user name, email address, or proxy address that include the domain name.</span></span>
* <span data-ttu-id="2c17f-135">Any group has an email address or proxy address that includes the domain name.</span><span class="sxs-lookup"><span data-stu-id="2c17f-135">Any group has an email address or proxy address that includes the domain name.</span></span>
* <span data-ttu-id="2c17f-136">Any application in your Azure AD has an app ID URI that includes the domain name.</span><span class="sxs-lookup"><span data-stu-id="2c17f-136">Any application in your Azure AD has an app ID URI that includes the domain name.</span></span>

<span data-ttu-id="2c17f-137">You must change or delete any such resource in your Azure AD directory before you can delete the custom domain name.</span><span class="sxs-lookup"><span data-stu-id="2c17f-137">You must change or delete any such resource in your Azure AD directory before you can delete the custom domain name.</span></span>

## <a name="use-powershell-or-graph-api-to-manage-domain-names"></a><span data-ttu-id="2c17f-138">Use PowerShell or Graph API to manage domain names</span><span class="sxs-lookup"><span data-stu-id="2c17f-138">Use PowerShell or Graph API to manage domain names</span></span>
<span data-ttu-id="2c17f-139">Most management tasks for domain names in Azure Active Directory can also be completed using Microsoft PowerShell, or programmatically using Azure AD Graph API (in public preview).</span><span class="sxs-lookup"><span data-stu-id="2c17f-139">Most management tasks for domain names in Azure Active Directory can also be completed using Microsoft PowerShell, or programmatically using Azure AD Graph API (in public preview).</span></span>

* [<span data-ttu-id="2c17f-140">Using PowerShell to manage domain names in Azure AD</span><span class="sxs-lookup"><span data-stu-id="2c17f-140">Using PowerShell to manage domain names in Azure AD</span></span>](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [<span data-ttu-id="2c17f-141">Using Graph API to manage domain names in Azure AD</span><span class="sxs-lookup"><span data-stu-id="2c17f-141">Using Graph API to manage domain names in Azure AD</span></span>](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a><span data-ttu-id="2c17f-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="2c17f-142">Next steps</span></span>
* [<span data-ttu-id="2c17f-143">Learn about domain names in Azure AD</span><span class="sxs-lookup"><span data-stu-id="2c17f-143">Learn about domain names in Azure AD</span></span>](active-directory-add-domain-concepts.md)
* [<span data-ttu-id="2c17f-144">Manage custom domain names</span><span class="sxs-lookup"><span data-stu-id="2c17f-144">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)

